# Unix y Biopython 

Vamos a trabajar con un genoma bacteriano real (en FASTA y
GenBank) y lecturas de secuenciación reales (FASTQ).

Si buscas una lista rápida de comandos sin explicación, revisa la
[guía rápida](#-Resumen-de-comandos-útiles-y-algunos-adicionales).

## Contenido

- [0. Preparación](#0-preparación)
- [1. Descargar los datos](#1-descargar-los-datos)
- [Parte A: FASTA con Unix](#parte-a-fasta-con-unix)
- [Parte B: Biopython](#parte-c-biopython)
- [Resumen de comandos](#resumen-de-comandos)

### Los datos

| Archivo | Qué es | Fuente |
|---|---|---|
| `smeliloti.fasta` | Genoma de *Sinorhizobium meliloti* 1021: un cromosoma y dos megaplásmidos (pSymA y pSymB) | NCBI RefSeq `NC_003047.1`, `NC_003037.1`, `NC_003078.1` |
| `smeliloti.gbk` | El mismo genoma en formato GenBank, con los genes anotados | NCBI RefSeq |
| `SRR2589044_1.fastq.gz`, `SRR2589044_2.fastq.gz` | Primeras 50,000 lecturas pareadas de Illumina (2 × 150 pb) de *Escherichia coli* B REL606 | ENA / SRA, corrida `SRR2589044` |

*S. meliloti* es una bacteria asociada a suelos que fija nitrógeno en simbiosis con la alfalfa. Su genoma tiene tres replicones, lo que lo hace un buen ejemplo para trabajar con archivos FASTA.

---

## 0. Preparación

**Necesitamos:** una terminal de Linux o macOS con `curl`, `gzip`, `awk` y `sed`
(vienen instalados), y Python 3 con Biopython para la Parte C:

```bash
conda create -n biopython -c conda-forge biopython -y
conda activate biopython

```

Crea una carpeta de trabajo con tres subcarpetas:

```bash
mkdir -p tutorial/{data,results,scripts} # al usar {} podemos crear múltiples carpetas
cd tutorial
```

- `data/` guarda los archivos descargados. No los modifiques nunca.
- `results/` guarda todo lo que vas a generar.
- `scripts/` guarda los scripts de Python.

Todos los comandos se corren desde dentro de la carpeta `tutorial/`.

---

## 1. Descargar los datos

### 1.1 Genoma en FASTA y GenBank

Con `curl` puedes descargar registros directamente de NCBI.

```bash
curl -s -o data/smeliloti.fasta \
  "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=NC_003047.1,NC_003037.1,NC_003078.1&rettype=fasta&retmode=text"

curl -s -o data/smeliloti.gbk \
  "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=NC_003047.1,NC_003037.1,NC_003078.1&rettype=gbwithparts&retmode=text"
```

- `-s` es modo silencioso (sin barra de progreso) y `-o` es el nombre del
  archivo de salida.
- `id=` lleva los tres accesos separados por comas.
- `rettype=fasta` descarga solo las secuencias. `rettype=gbwithparts`
  descarga el registro GenBank completo, con secuencia y anotaciones.

### 1.2 Lecturas de secuenciación (FASTQ)

La corrida completa pesa unos 130 MB por archivo. Para que todo sea rápido,
solo guardamos las primeras **50,000 lecturas**. Cada lectura ocupa 4 líneas,
así que son 200,000 líneas.

```bash
for r in 1 2; do
  curl -s "https://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_${r}.fastq.gz" \
    | zcat 2>/dev/null | head -n 200000 | gzip > data/SRR2589044_${r}.fastq.gz
done
```

- `curl` descarga el archivo y lo pasa directamente por la tubería (`|`).
- `zcat` lo descomprime.
- `head -n 200000` se queda solo con las primeras 200,000 líneas.
- `gzip` las vuelve a comprimir y `>` las guarda.
- `2>/dev/null` oculta un aviso sin importancia que aparece cuando `head` deja
  de leer antes de que termine la descarga.

### 1.3 Revisar las descargas

```bash
ls -lh data/
```

**Resultado:**
```text
-rw-r--r-- 1 user user 6.5M smeliloti.fasta
-rw-r--r-- 1 user user  17M smeliloti.gbk
-rw-r--r-- 1 user user 5.9M SRR2589044_1.fastq.gz
-rw-r--r-- 1 user user 6.0M SRR2589044_2.fastq.gz
```

---

## Parte A: Manipulación de archivos fasta

Un archivo FASTA tiene un **header** que empieza con `>`, seguida
de una o varias líneas de secuencia:

```text
>NC_003047.1 Sinorhizobium meliloti 1021, complete sequence
CAGCCAGATGGGGGGAGGGGTGAGCGCTCTCCCGCTCAAAACCTCCAGCACTTTGCGATG
ACTTGCCGCTTCCTAATCTAAAAATAAAACTGAATTTATAAGGTTTCTATTTCTTAGAGT
...
```

### A1. ¿Cuántas secuencias hay?

Cuenta las líneas que empiezan con `>`.

```bash
grep -c "^>" data/smeliloti.fasta
```

- `^` significa "inicio de línea", así que `^>` solo encuentra encabezados.
- `-c` cuenta las líneas en lugar de mostrarlas.

**Resultado:**
```text
3
```

### A2. ¿Cómo se llaman?

```bash
grep "^>" data/smeliloti.fasta
```

**Resultado:**
```text
>NC_003047.1 Sinorhizobium meliloti 1021, complete sequence
>NC_003037.1 Sinorhizobium meliloti 1021 plasmid pSymA, complete sequence
>NC_003078.1 Sinorhizobium meliloti 1021 plasmid pSymB, complete sequence
```

Para quedarte solo con los IDs (la primera palabra, sin `>`):

```bash
grep "^>" data/smeliloti.fasta | cut -d' ' -f1 | tr -d '>'
```

- `cut -d' ' -f1` separa por espacios y se queda con el campo 1.
- `tr -d '>'` borra el símbolo `>`.

**Resultado:**
```text
NC_003047.1
NC_003037.1
NC_003078.1
```

### A3. ¿Qué tan larga es cada secuencia?

```bash
awk -v OFS='\t' '/^>/ {id = substr($1, 2); next}
                 {print id, length($0)}' results/smeliloti.linear.fasta > results/lengths.tsv

cat results/lengths.tsv
```

`awk` lee el archivo línea por línea:
- Si la línea es un encabezado (`/^>/`), guarda el ID en `id`.
  `substr($1, 2)` toma la primera palabra desde la letra 2, o sea, sin el `>`.
  `next` pasa a la siguiente línea.
- Si es una secuencia, imprime el ID y la longitud de la línea (`length($0)`).
- `-v OFS='\t'` hace que las columnas de salida se separen con tabulador.

**Resultado:**
```text
NC_003047.1	3654135
NC_003037.1	1354226
NC_003078.1	1683333
```

El cromosoma mide unas 3.65 Mb, pSymA 1.35 Mb y pSymB 1.68 Mb.

### A4. Tamaño total del genoma

Quita los encabezados y los saltos de línea, y cuenta los caracteres.

```bash
grep -v "^>" data/smeliloti.fasta | tr -d '\n' | wc -c
```

- `grep -v` se queda con las líneas que **no** coinciden, o sea, quita los
  encabezados.
- `tr -d '\n'` borra todos los saltos de línea.
- `wc -c` cuenta los caracteres.

**Resultado:**
```text
6691694
```

### A5. Contenido de GC de cada secuencia

```bash
awk -v OFS='\t' '/^>/ {id = substr($1, 2); next}
                 {total = length($0); gc = gsub(/[GC]/, ""); print id, 100 * gc / total}' \
    results/smeliloti.linear.fasta > results/gc.tsv

cat results/gc.tsv
```

- `total` guarda la longitud de la secuencia.
- `gsub(/[GC]/, "")` borra todas las G y C, y **devuelve cuántas borró**. Ese
  número es la cantidad de GC.
- `100 * gc / total` es el porcentaje.

**Resultado:**
```text
NC_003047.1	62.7289
NC_003037.1	60.3687
NC_003078.1	62.4219
```

pSymA tiene un GC claramente menor que el cromosoma.

### A6. Simplificar los encabezados

Muchos programas fallan con encabezados largos que tienen espacios. Para dejar
solo la primera palabra:

```bash
sed '/^>/ s/ .*//' data/smeliloti.fasta > results/smeliloti.short.fasta
grep "^>" results/smeliloti.short.fasta
```

- `/^>/` aplica el cambio solo a las líneas de encabezado.
- `s/ .*//` reemplaza todo lo que va desde el primer espacio hasta el final de
  la línea por nada.

**Resultado:**
```text
>NC_003047.1
>NC_003037.1
>NC_003078.1
```

---

## Parte B: Biopython

Guarda cada script en la carpeta `scripts/` y córrelo desde la carpeta
`tutorial/`:

```bash
python3 scripts/c1_resumen_fasta.py
```

### C1. Leer un FASTA: ID, longitud y GC

`scripts/c1_resumen_fasta.py`
```python
from Bio import SeqIO
from Bio.SeqUtils import gc_fraction

for record in SeqIO.parse("data/smeliloti.fasta", "fasta"):
    gc = gc_fraction(record.seq) * 100
    print(record.id, len(record.seq), round(gc, 2))
```

- `SeqIO.parse(archivo, formato)` lee las secuencias una por una.
- Cada `record` tiene `.id` (la primera palabra del encabezado),
  `.description` (el encabezado completo) y `.seq` (la secuencia).
- `gc_fraction` devuelve el GC como fracción (0 a 1). Por eso lo multiplicamos
  por 100.
- `round(gc, 2)` redondea a 2 decimales.

**Resultado:**
```text
NC_003047.1 3654135 62.73
NC_003037.1 1354226 60.37
NC_003078.1 1683333 62.42
```

Deberían ser los mismos valores que obtuvimos con Unix.

### C2. Filtrar secuencias y guardarlas en un FASTA nuevo

Guardar solo los plásmidos.

`scripts/c2_filtrar_plasmidos.py`
```python
from Bio import SeqIO

plasmidos = []
for record in SeqIO.parse("data/smeliloti.fasta", "fasta"):
    if "plasmid" in record.description:
        plasmidos.append(record)

SeqIO.write(plasmidos, "results/plasmidos.fasta", "fasta")
print("Secuencias guardadas:", len(plasmidos))
```

- `plasmidos = []` crea una lista vacía.
- `.append(record)` agrega a la lista cada secuencia cuyo encabezado contiene
  la palabra "plasmid".
- `SeqIO.write(lista, archivo, formato)` guarda la lista en un archivo.

**Resultado:**
```text
Secuencias guardadas: 2
```

### C3. Operaciones con una secuencia

`scripts/c3_operaciones_seq.py`
```python
from Bio.Seq import Seq

dna = Seq("ATGAAACGCATTAGCACCACCATTACCACCACCATCACCATTACCACAGGTAACGGTGCGGGCTGA")

print("Longitud:             ", len(dna))
print("Complemento:          ", dna.complement())
print("Complemento reverso:  ", dna.reverse_complement())
print("ARN:                  ", dna.transcribe())
print("Proteína:             ", dna.translate(table=11))
print("Proteína (hasta stop):", dna.translate(table=11, to_stop=True))
```

`table=11` es el código genético de bacterias. `to_stop=True` se detiene en el
primer codón de paro en lugar de escribir `*`.

**Resultado:**
```text
Longitud:              66
Complemento:           TACTTTGCGTAATCGTGGTGGTAATGGTGGTGGTAGTGGTAATGGTGTCCATTGCCACGCCCGACT
Complemento reverso:   TCAGCCCGCACCGTTACCTGTGGTAATGGTGATGGTGGTGGTAATGGTGGTGCTAATGCGTTTCAT
ARN:                   AUGAAACGCAUUAGCACCACCAUUACCACCACCAUCACCAUUACCACAGGUAACGGUGCGGGCUGA
Proteína:              MKRISTTITTTITITTGNGAG*
Proteína (hasta stop): MKRISTTITTTITITTGNGAG
```

### C4. Leer un GenBank: contar genes

Un archivo GenBank tiene la secuencia y además las **features**: los genes,
CDS, rRNA, tRNA, etc. que están anotados.

`scripts/c4_contar_genes.py`
```python
from Bio import SeqIO

for record in SeqIO.parse("data/smeliloti.gbk", "genbank"):
    cds = 0
    rrna = 0
    trna = 0
    for feature in record.features:
        if feature.type == "CDS":
            cds = cds + 1
        if feature.type == "rRNA":
            rrna = rrna + 1
        if feature.type == "tRNA":
            trna = trna + 1
    print(record.id, "CDS:", cds, "rRNA:", rrna, "tRNA:", trna)
```

- `record.features` es la lista de todo lo anotado en esa secuencia.
- `feature.type` dice qué es cada feature (`"CDS"`, `"rRNA"`, `"tRNA"`, `"gene"`…).
- Para cada replicón, los contadores empiezan en 0 y suben de 1 en 1.

**Resultado:**
```text
NC_003047.1 CDS: 3396 rRNA: 9 tRNA: 52
NC_003037.1 CDS: 1333 rRNA: 0 tRNA: 2
NC_003078.1 CDS: 1557 rRNA: 0 tRNA: 1
```

Casi todos los rRNA y tRNA están en el cromosoma.

---

## Resumen de comandos útiles y algunos adicionales

| Tarea | Comando |
|---|---|
| Contar secuencias en un FASTA | `grep -c "^>" archivo.fasta` |
| Listar IDs | `grep "^>" archivo.fasta \| cut -d' ' -f1 \| tr -d '>'` |
| Extraer una secuencia (FASTA linealizado) | `grep -A 1 "^>ID" archivo.fasta` |
| Contar lecturas en un FASTQ | `echo $(( $(zcat archivo.fastq.gz \| wc -l) / 4 ))` |
| Secuencias de un FASTQ | `sed -n '2~4p'` |
| Ver un archivo `.gz` | `zcat archivo.gz \| head` |
| Líneas que coinciden / que no coinciden | `grep "x"` / `grep -v "x"` |
| Elegir columnas | `cut -f1,3` |
| Contar valores | `sort \| uniq -c \| sort -nr` |
| Ordenar por una columna numérica | `sort -t $'\t' -k2,2nr` |
| Buscar y reemplazar | `sed 's/viejo/nuevo/'` |
| Quitar el encabezado | `tail -n +2` |
| Juntar tablas lado a lado | `paste tabla1.tsv tabla2.tsv` |
| Repetir para muchos archivos | `for f in *.fasta; do ...; done` |
| Leer secuencias en Python | `SeqIO.parse(archivo, "fasta")` |
| Guardar secuencias en Python | `SeqIO.write(lista, archivo, "fasta")` |
| Features de un GenBank | `for feature in record.features:` |
| Calidades de un FASTQ | `record.letter_annotations["phred_quality"]` |
