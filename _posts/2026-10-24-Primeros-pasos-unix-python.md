# Tutorial guiado: Unix y Biopython con datos reales

Un tutorial práctico. Vas a descargar un genoma bacteriano real (en FASTA y
GenBank) y lecturas de secuenciación reales (FASTQ), y luego las vas a explorar
paso a paso: primero con comandos de Unix, después con Biopython y al final
combinando ambos.

Cada ejercicio muestra el comando, explica qué hace e incluye el **resultado
esperado**, para que puedas comparar tu salida.

Si buscas una lista rápida de comandos sin explicación, revisa la
[guía rápida](README.md).

## Contenido

- [0. Preparación](#0-preparación)
- [1. Descargar los datos](#1-descargar-los-datos)
- [Parte A: FASTA con Unix](#parte-a-fasta-con-unix)
- [Parte B: FASTQ con Unix](#parte-b-fastq-con-unix)
- [Parte C: Biopython](#parte-c-biopython)
- [Parte D: Unix + Biopython: analizar una tabla de genes](#parte-d-unix--biopython-analizar-una-tabla-de-genes)
- [Resumen de comandos](#resumen-de-comandos)

### Los datos

| Archivo | Qué es | Fuente |
|---|---|---|
| `smeliloti.fasta` | Genoma de *Sinorhizobium meliloti* 1021: un cromosoma y dos megaplásmidos (pSymA y pSymB) | NCBI RefSeq `NC_003047.1`, `NC_003037.1`, `NC_003078.1` |
| `smeliloti.gbk` | El mismo genoma en formato GenBank, con los genes anotados | NCBI RefSeq |
| `SRR2589044_1.fastq.gz`, `SRR2589044_2.fastq.gz` | Primeras 50,000 lecturas pareadas de Illumina (2 × 150 pb) de *Escherichia coli* B REL606 | ENA / SRA, corrida `SRR2589044` |

*S. meliloti* es una bacteria del suelo que fija nitrógeno en simbiosis con la
alfalfa. Su genoma tiene tres replicones, lo que lo hace un buen ejemplo para
trabajar con archivos FASTA.

---

## 0. Preparación

**Necesitas:** una terminal de Linux o macOS con `curl`, `gzip`, `awk` y `sed`
(vienen instalados), y Python 3 con Biopython para la Parte C:

```bash
pip install biopython
# o: conda install -c conda-forge biopython
```

Crea una carpeta de trabajo con tres subcarpetas:

```bash
mkdir -p tutorial/{data,results,scripts}
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

## Parte A: FASTA con Unix

Un archivo FASTA tiene una **línea de encabezado** que empieza con `>`, seguida
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

### A3. Poner cada secuencia en una sola línea

En el archivo original, cada secuencia está repartida en miles de líneas de 70
letras. Casi todo es más fácil si cada secuencia queda en **una sola línea**.
A esto se le llama "linealizar" el FASTA.

```bash
awk '/^>/ {printf("%s%s\n", (n++ ? "\n" : ""), $0); next}
     {printf("%s", $0)}
     END {printf("\n")}' data/smeliloti.fasta > results/smeliloti.linear.fasta
```

No hace falta entender cada detalle de este comando. La idea es:
- los encabezados (`/^>/`) se imprimen en su propia línea;
- las líneas de secuencia se imprimen **sin salto de línea**, así que se pegan
  unas con otras.

Revisa el resultado:

```bash
wc -l results/smeliloti.linear.fasta
cut -c1-60 results/smeliloti.linear.fasta
```

`cut -c1-60` muestra solo los primeros 60 caracteres de cada línea, para no
llenar la pantalla con millones de bases.

**Resultado:**
```text
6 results/smeliloti.linear.fasta
>NC_003047.1 Sinorhizobium meliloti 1021, complete sequence
CAGCCAGATGGGGGGAGGGGTGAGCGCTCTCCCGCTCAAAACCTCCAGCACTTTGCGATG
>NC_003037.1 Sinorhizobium meliloti 1021 plasmid pSymA, comp
GGAACTTGGCGGCGTGCCGACCGTAGCTCCGTTGATGCGACCATCTACGGCAGGTGTGAG
>NC_003078.1 Sinorhizobium meliloti 1021 plasmid pSymB, comp
ATGGACATTCAGACGCGTGCCTATCTGCCGCGTATCGCCGGGCTGGCTCTCGCGGGCGCA
```

Ahora el archivo tiene 6 líneas: 3 encabezados y 3 secuencias. En los
siguientes ejercicios usamos este archivo.

### A4. ¿Qué tan larga es cada secuencia?

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

### A5. Tamaño total del genoma

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

### A6. Contenido de GC de cada secuencia

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

### A7. Extraer una secuencia por su ID

Como el archivo está linealizado, cada secuencia es exactamente la línea
siguiente a su encabezado. `grep -A 1` muestra la línea encontrada **y la
siguiente**:

```bash
grep -A 1 "^>NC_003037.1" results/smeliloti.linear.fasta > results/pSymA.fasta

grep -c "^>" results/pSymA.fasta
cut -c1-70 results/pSymA.fasta
```

**Resultado:**
```text
1
>NC_003037.1 Sinorhizobium meliloti 1021 plasmid pSymA, complete seque
GGAACTTGGCGGCGTGCCGACCGTAGCTCCGTTGATGCGACCATCTACGGCAGGTGTGAGATGCCGGTAT
```

Para extraer **varias** secuencias, pon los IDs en un archivo, uno por línea:

```bash
printf "NC_003037.1\nNC_003078.1\n" > results/ids.txt

grep -A 1 -F -f results/ids.txt results/smeliloti.linear.fasta | grep -v "^--$" > results/plasmids.fasta

grep "^>" results/plasmids.fasta
```

- `-f results/ids.txt` busca todos los textos que estén en ese archivo.
- `-F` trata los IDs como texto literal, no como expresiones regulares. Así el
  punto de `NC_003037.1` no se interpreta como "cualquier carácter".
- `grep -A` pone una línea `--` entre grupos de resultados.
  `grep -v "^--$"` la elimina.

**Resultado:**
```text
>NC_003037.1 Sinorhizobium meliloti 1021 plasmid pSymA, complete sequence
>NC_003078.1 Sinorhizobium meliloti 1021 plasmid pSymB, complete sequence
```

### A8. Separar el FASTA en un archivo por secuencia

Aquí usamos un **loop**: repetimos el mismo comando para cada ID.

```bash
mkdir -p results/split

for id in $(grep "^>" results/smeliloti.linear.fasta | cut -d' ' -f1 | tr -d '>'); do
    grep -A 1 "^>$id" results/smeliloti.linear.fasta > results/split/$id.fasta
done

ls results/split
```

- `$( ... )` ejecuta el comando de A2 y devuelve la lista de IDs.
- `for id in ...; do ...; done` repite el bloque una vez por cada ID, guardando
  el ID actual en `$id`.
- Dentro del loop, el comando de A7 extrae esa secuencia a su propio archivo.

**Resultado:**
```text
NC_003037.1.fasta
NC_003047.1.fasta
NC_003078.1.fasta
```

### A9. Recorrer archivos con un loop

Ahora el loop recorre **archivos**. Para cada uno, imprime su nombre y su
número de bases.

```bash
for f in results/split/*.fasta; do
    name=$(basename "$f" .fasta)
    bases=$(grep -v "^>" "$f" | tr -d '\n' | wc -c)
    echo -e "$name\t$bases"
done
```

- `results/split/*.fasta` significa "todos los archivos que terminan en
  `.fasta` en esa carpeta".
- `basename "$f" .fasta` quita la carpeta y la extensión:
  `results/split/NC_003037.1.fasta` queda como `NC_003037.1`.
- `bases=$( ... )` guarda en una variable el resultado del comando de A5.
- `echo -e` hace que `\t` se imprima como tabulador.

**Resultado:**
```text
NC_003037.1	1354226
NC_003047.1	3654135
NC_003078.1	1683333
```

### A10. Simplificar los encabezados

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

### A11. Buscar un motivo

¿Cuántas veces aparece el sitio de restricción de EcoRI (`GAATTC`) en cada
secuencia?

```bash
for f in results/split/*.fasta; do
    name=$(basename "$f" .fasta)
    n=$(grep -v "^>" "$f" | grep -o "GAATTC" | wc -l)
    echo -e "$name\t$n"
done
```

- `grep -o` imprime **cada coincidencia** en su propia línea, así que `wc -l`
  cuenta coincidencias y no líneas.
- Usamos los archivos linealizados. En el FASTA original, un sitio que quede
  partido entre dos líneas no se encontraría.

`GAATTC` es igual a su propio complemento reverso, así que estos conteos ya
incluyen las dos hebras.

**Resultado:**
```text
NC_003037.1	422
NC_003047.1	1225
NC_003078.1	605
```

### A12. Juntar dos tablas

Las tablas de A4 (longitud) y A6 (GC) tienen las secuencias en el mismo orden,
así que `paste` las puede poner lado a lado:

```bash
paste results/lengths.tsv results/gc.tsv
```

**Resultado:**
```text
NC_003047.1	3654135	NC_003047.1	62.7289
NC_003037.1	1354226	NC_003037.1	60.3687
NC_003078.1	1683333	NC_003078.1	62.4219
```

El ID aparece dos veces. Con `cut` nos quedamos con las columnas 1, 2 y 4, y
con `sort` ordenamos de la secuencia más larga a la más corta:

```bash
paste results/lengths.tsv results/gc.tsv | cut -f 1,2,4 | sort -k2,2nr > results/summary.tsv
cat results/summary.tsv
```

`sort -k2,2nr` ordena por la columna 2, como número (`n`) y de mayor a menor
(`r`).

**Resultado:**
```text
NC_003047.1	3654135	62.7289
NC_003078.1	1683333	62.4219
NC_003037.1	1354226	60.3687
```

### A13. Complemento reverso de una secuencia corta

```bash
echo "ATGAAACGCATTAGCACCACC" | rev | tr ACGT TGCA
```

- `rev` invierte el texto.
- `tr ACGT TGCA` cambia cada base por su complemento: A↔T y C↔G.

**Resultado:**
```text
GGTGGTGCTAATGCGTTTCAT
```

---

## Parte B: FASTQ con Unix

En un archivo FASTQ, cada lectura ocupa **exactamente 4 líneas**:

| Línea | Contenido |
|---|---|
| 1 | Encabezado, empieza con `@` |
| 2 | Secuencia |
| 3 | `+` |
| 4 | Calidades, un carácter por base |

Nuestros archivos están comprimidos (`.gz`). `zcat` los descomprime en
pantalla sin modificar el archivo.

### B1. Ver la primera lectura

```bash
zcat data/SRR2589044_1.fastq.gz | head -n 4
```

**Resultado:**
```text
@SRR2589044.1 HWI-ST957:244:H73TDADXX:1:1101:10469:2228/1
GTGGAAACCAGCGACGGTGACGGCTATATCAACTGCGTGATTGAACATCAAAGCTCTGCAGAAAAGAATATGGCTTTTCGGCTAATGCGCTATGCCACTGCCGCCATGCAGCGTCACCTGGATAACTGTCTCTTATACACATCTCCGAGC
+
BBBFFFFFHHHHHJJJJIIGIIJJJJJGIJJIJJJIJIJGHIIJIIFFFGHHFFFFFEEEEEEDDDDDDDEEDCDDDDDD@BDDDDDDDDBDDDDDDDDDCABDDDDCDDCCDBDDDDDDDBDEDDDCCDCDCDDDDCDDDCDDDD@DDD
```

El `/1` al final del encabezado indica que es la lectura 1 del par. La misma
lectura en el archivo `_2` termina en `/2`.

### B2. Contar lecturas

Cuenta las líneas y divide entre 4.

```bash
echo $(( $(zcat data/SRR2589044_1.fastq.gz | wc -l) / 4 ))
```

- `$( ... )` ejecuta el comando y pone su resultado en ese lugar.
- `$(( ... ))` hace operaciones con números enteros.

**Resultado:**
```text
50000
```

### B3. Contar lecturas en todos los archivos

Los archivos de un par (R1 y R2) deben tener el mismo número de lecturas. Con
un loop revisas todos a la vez:

```bash
for f in data/*.fastq.gz; do
    n=$(( $(zcat "$f" | wc -l) / 4 ))
    echo -e "$f\t$n"
done
```

**Resultado:**
```text
data/SRR2589044_1.fastq.gz	50000
data/SRR2589044_2.fastq.gz	50000
```

### B4. Quedarse solo con las secuencias

Las secuencias están en las líneas 2, 6, 10, 14… `sed -n '2~4p'` imprime la
línea 2 y después una de cada 4:

```bash
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' | head -n 2
```

- `sed -n` no imprime nada a menos que se lo pidas.
- `2~4` significa "empezando en la línea 2, cada 4 líneas".
- `p` imprime esas líneas.

**Resultado** (recortado a 60 caracteres):
```text
GTGGAAACCAGCGACGGTGACGGCTATATCAACTGCGTGATTGAACATCAAAGCTCTGCA
GCAATATTACCGGGCGACATCGCCGAAGATGACATCACAGCGGTACTCTGTTTTGTGATT
```

Este truco es la base de los siguientes ejercicios.

### B5. Longitud de las lecturas

```bash
# Cuántas lecturas hay de cada longitud
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' | awk '{print length($0)}' | sort -n | uniq -c

# Resumen
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' \
    | awk '{bases += length($0)} END {print "reads:", NR, "bases:", bases, "mean:", bases/NR}'
```

- `awk '{print length($0)}'` imprime la longitud de cada secuencia.
- `sort -n | uniq -c` cuenta cuántas veces aparece cada longitud.
- En el resumen, `bases` va sumando las longitudes. Al final (`END`), `NR` es el
  número de líneas leídas, o sea, el número de lecturas.

**Resultado:**
```text
  50000 150
reads: 50000 bases: 7500000 mean: 150
```

Todas las lecturas miden 150 pb porque todavía no se han recortado. Después de
quitar adaptadores, las longitudes varían mucho más.

### B6. Contenido de GC de las lecturas

```bash
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' \
    | awk '{total += length($0); gc += gsub(/[GC]/, "")} END {print 100 * gc / total}'
```

Es la misma idea que en A6, pero sumando todas las lecturas.

**Resultado:**
```text
50.4053
```

Coincide con el GC del genoma de *E. coli* (alrededor de 50.8%).

### B7. Buscar contaminación con adaptadores

Las librerías Nextera usan la secuencia `CTGTCTCTTATACACATCT`. Si el fragmento
de ADN es más corto que la lectura, el secuenciador termina leyendo el
adaptador. Puedes verlo cerca del final de la lectura de B1.

```bash
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' | grep -c "CTGTCTCTTATACACATCT"
```

**Resultado:**
```text
6771
```

Alrededor del 13.5% de las lecturas (6,771 de 50,000) tienen el adaptador.
Hay que recortarlas (por ejemplo con `fastp` o `cutadapt`) antes de ensamblar
o mapear.

### B8. Lecturas con bases N y lecturas repetidas

```bash
# Lecturas que tienen al menos una N
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' | grep -c "N"

# Las secuencias más repetidas
zcat data/SRR2589044_1.fastq.gz | sed -n '2~4p' | sort | uniq -c | sort -nr | head -n 3
```

`sort | uniq -c | sort -nr` es una combinación muy útil: cuenta cuántas veces
aparece cada línea y ordena de la más frecuente a la menos frecuente.

**Resultado** (secuencias recortadas):
```text
34
      4 CTTCCATACCGATCAGACCATTGTCAACCAGTACGGTGTTGCCAACAGACAGGTCAGTAGTG
      3 GTTCATCACTGGTCTTTCCGAAAGGCTGTAAGAAATAACTTCGTTGTTGAAGAGATCTATTA
      3 GTCACACATTGGTCGTAGCCCGTCACTGTTTGTTAATGCCGCCACCTGGGGGCTGCTGTTTA
```

Muy pocas lecturas tienen N, y ninguna secuencia aparece más de 4 veces, así
que esta librería tiene poca duplicación.

### B9. Convertir FASTQ a FASTA

```bash
zcat data/SRR2589044_1.fastq.gz | sed -n '1~4s/^@/>/p; 2~4p' > results/SRR2589044_1.fasta

head -n 4 results/SRR2589044_1.fasta
grep -c "^>" results/SRR2589044_1.fasta
```

- `1~4s/^@/>/p`: en las líneas 1, 5, 9… (los encabezados), cambia `@` por `>`
  y las imprime.
- `2~4p`: imprime las líneas 2, 6, 10… (las secuencias).
- Las líneas `+` y las calidades no se imprimen.

**Resultado:**
```text
>SRR2589044.1 HWI-ST957:244:H73TDADXX:1:1101:10469:2228/1
GTGGAAACCAGCGACGGTGACGGCTATATCAACTGCGTGATTGAACATCAAAGCTCTGCAGAAAAGAATATGGCTTTTCGGCTAATGCGCTATGCCACTGCCGCCATGCAGCGTCACCTGGATAACTGTCTCTTATACACATCTCCGAGC
>SRR2589044.2 HWI-ST957:244:H73TDADXX:1:1101:10877:2125/1
GCAATATTACCGGGCGACATCGCCGAAGATGACATCACAGCGGTACTCTGTTTTGTGATTGAAGCCGATCAGATTACCTTTGAAACAGTAGAAGTCTCGCCAAAAATATCCACCCCACCAGTGCTTAAACTGGCAGCCGAACAAGCGCCA
50000
```

### B10. Crear un archivo de prueba pequeño

Probar un análisis con un archivo pequeño antes de usar el completo ahorra
mucho tiempo. 1,000 lecturas son 4,000 líneas:

```bash
zcat data/SRR2589044_1.fastq.gz | head -n 4000 | gzip > results/test_1000reads.fastq.gz
echo $(( $(zcat results/test_1000reads.fastq.gz | wc -l) / 4 ))
```

**Resultado:**
```text
1000
```

---

## Parte C: Biopython

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

Son los mismos valores que obtuvimos con Unix en A4 y A6.

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

### C5. Crear una tabla de genes a partir de un GenBank

Una fila por cada gen que codifica proteína, con el replicón, el locus tag, las
coordenadas, la hebra, la longitud de la proteína y su función.

`scripts/c5_tabla_genes.py`
```python
from Bio import SeqIO

salida = open("results/tabla_genes.tsv", "w")
salida.write("replicon\tlocus_tag\tinicio\tfin\thebra\tlongitud_aa\tproducto\n")

for record in SeqIO.parse("data/smeliloti.gbk", "genbank"):
    for feature in record.features:
        # solo genes que codifican proteína (los pseudogenes no tienen "translation")
        if feature.type == "CDS" and "translation" in feature.qualifiers:
            locus = feature.qualifiers["locus_tag"][0]
            producto = feature.qualifiers["product"][0]
            proteina = feature.qualifiers["translation"][0]
            inicio = feature.location.start + 1    # Biopython empieza a contar en 0
            fin = feature.location.end
            hebra = feature.location.strand        # 1 = hebra +, -1 = hebra -
            salida.write(f"{record.id}\t{locus}\t{inicio}\t{fin}\t{hebra}\t{len(proteina)}\t{producto}\n")

salida.close()
```

- `open(archivo, "w")` abre un archivo para escribir y `.close()` lo cierra al
  final.
- `feature.qualifiers` es un diccionario con la información del gen. Cada
  valor es una **lista**, por eso se usa `[0]` para sacar el texto.
- `f"...{variable}..."` (un *f-string*) mete el valor de cada variable dentro
  del texto. `\t` es un tabulador y `\n` un salto de línea.

Revisa el resultado:

```bash
head -n 4 results/tabla_genes.tsv
wc -l results/tabla_genes.tsv
```

**Resultado:**
```text
replicon	locus_tag	inicio	fin	hebra	longitud_aa	producto
NC_003047.1	SM_RS00005	1	3654135	-1	343	uroporphyrinogen decarboxylase
NC_003047.1	SM_RS00010	478	1299	1	273	pyruvate, water dikinase regulatory protein
NC_003047.1	SM_RS00015	1347	1946	1	199	Maf-like protein
5985 results/tabla_genes.tsv
```

Son 5,984 genes más la línea de encabezado. El primer gen aparece con
`inicio=1` y `fin=3654135` porque **cruza el origen** del cromosoma circular:
una parte está al final de la secuencia y otra al principio.

### C6. Extraer proteínas de interés a un FASTA

Vamos a sacar todas las proteínas *nod* (de nodulación), que la bacteria usa
para comunicarse con la planta.

`scripts/c6_proteinas_nod.py`
```python
from Bio import SeqIO
from Bio.Seq import Seq
from Bio.SeqRecord import SeqRecord

proteinas = []
for record in SeqIO.parse("data/smeliloti.gbk", "genbank"):
    for feature in record.features:
        if feature.type == "CDS" and "gene" in feature.qualifiers and "translation" in feature.qualifiers:
            gen = feature.qualifiers["gene"][0]
            if gen.startswith("nod"):
                nueva = SeqRecord(Seq(feature.qualifiers["translation"][0]),
                                  id=feature.qualifiers["locus_tag"][0],
                                  description=gen)
                proteinas.append(nueva)

SeqIO.write(proteinas, "results/proteinas_nod.faa", "fasta")
print("Proteínas nod guardadas:", len(proteinas))
```

- No todos los CDS tienen nombre de gen. Por eso primero revisamos que
  `"gene"` exista.
- `gen.startswith("nod")` es verdadero si el nombre empieza con "nod".
- `SeqRecord(...)` crea una secuencia nueva con su ID y descripción, lista para
  guardar con `SeqIO.write`.

```bash
python3 scripts/c6_proteinas_nod.py
grep "^>" results/proteinas_nod.faa | head -n 5
```

**Resultado:**
```text
Proteínas nod guardadas: 11
>SM_RS26775 nodD2
>SM_RS26830 nodL
>SM_RS27050 nodD3
>SM_RS27090 nodQ
>SM_RS27105 nodI
```

### C7. Leer las calidades de un FASTQ

Biopython convierte los caracteres de calidad en **valores Phred**. Q30
significa una probabilidad de 1 en 1,000 de que la base esté mal leída.

`scripts/c7_calidad_fastq.py`
```python
import gzip
from Bio import SeqIO

archivo = gzip.open("data/SRR2589044_1.fastq.gz", "rt")

contador = 0
for record in SeqIO.parse(archivo, "fastq"):
    calidades = record.letter_annotations["phred_quality"]
    promedio = sum(calidades) / len(calidades)
    print(record.id, "Q promedio:", round(promedio, 1), "Q mínima:", min(calidades))
    contador = contador + 1
    if contador == 5:
        break

archivo.close()
```

- `gzip.open(..., "rt")` abre un archivo comprimido como texto (`r` = leer,
  `t` = texto).
- `calidades` es una lista de números, uno por base.
- `break` detiene el loop. Aquí paramos después de 5 lecturas.

**Resultado:**
```text
SRR2589044.1 Q promedio: 36.4 Q mínima: 31
SRR2589044.2 Q promedio: 33.0 Q mínima: 6
SRR2589044.3 Q promedio: 35.8 Q mínima: 33
SRR2589044.4 Q promedio: 36.6 Q mínima: 29
SRR2589044.5 Q promedio: 19.5 Q mínima: 2
```

La lectura 5 tiene mala calidad (Q promedio de 19.5).

### C8. Filtrar lecturas por calidad

Guardar solo las lecturas con una calidad promedio de al menos 30.

`scripts/c8_filtrar_calidad.py`
```python
import gzip
from Bio import SeqIO

entrada = gzip.open("data/SRR2589044_1.fastq.gz", "rt")

buenas = []
total = 0
for record in SeqIO.parse(entrada, "fastq"):
    total = total + 1
    calidades = record.letter_annotations["phred_quality"]
    promedio = sum(calidades) / len(calidades)
    if promedio >= 30:
        buenas.append(record)
entrada.close()

salida = gzip.open("results/SRR2589044_1.q30.fastq.gz", "wt")
SeqIO.write(buenas, salida, "fastq")
salida.close()

print("Lecturas totales:", total)
print("Lecturas con Q promedio >= 30:", len(buenas))
```

`gzip.open(..., "wt")` abre un archivo comprimido para escribir texto (`w` =
escribir).

**Resultado:**
```text
Lecturas totales: 50000
Lecturas con Q promedio >= 30: 38534
```

Se conserva el 77% de las lecturas. Este filtro sirve para aprender, pero con
datos reales conviene usar un programa como `fastp`, que también quita
adaptadores y procesa los dos archivos del par juntos.

---

## Parte D: Unix + Biopython: analizar una tabla de genes

La tabla que creaste con Biopython en C5 es un archivo de texto con columnas
separadas por tabuladores. Con comandos de Unix puedes responder preguntas
sobre ella muy rápido.

Columnas de `results/tabla_genes.tsv`:

| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|
| replicon | locus_tag | inicio | fin | hebra | longitud_aa | producto |

### D1. ¿Cuántos genes hay en cada replicón?

```bash
tail -n +2 results/tabla_genes.tsv | cut -f1 | sort | uniq -c
```

- `tail -n +2` muestra desde la línea 2, o sea, quita el encabezado.
- `cut -f1` se queda con la columna del replicón.
- `sort | uniq -c` cuenta cuántas veces aparece cada uno.

**Resultado:**
```text
   1180 NC_003037.1
   3329 NC_003047.1
   1475 NC_003078.1
```

### D2. Genes en cada hebra, por replicón

```bash
tail -n +2 results/tabla_genes.tsv | cut -f1,5 | sort | uniq -c
```

Ahora contamos combinaciones de dos columnas: replicón y hebra.

**Resultado:**
```text
    571 NC_003037.1	-1
    609 NC_003037.1	1
   1617 NC_003047.1	-1
   1712 NC_003047.1	1
    716 NC_003078.1	-1
    759 NC_003078.1	1
```

### D3. Las 5 proteínas más largas

```bash
tail -n +2 results/tabla_genes.tsv | sort -t $'\t' -k6,6nr | head -n 5 | cut -f1,2,6,7
```

- `sort -k6,6nr` ordena por la columna 6 (longitud), como número y de mayor a
  menor.
- `-t $'\t'` le dice a `sort` que las columnas están separadas por tabulador.
  Hace falta porque la columna de producto tiene espacios.

**Resultado:**
```text
NC_003047.1	SM_RS16840	2832	cyclic beta-(1,2)-glucan synthase
NC_003047.1	SM_RS02940	2504	type I polyketide synthase
NC_003078.1	SM_RS21975	2288	autotransporter
NC_003047.1	SM_RS09335	2089	apolipoprotein A-IV repeat region-like domain-containing protein
NC_003047.1	SM_RS15355	1869	translocation/assembly module TamB domain-containing protein
```

### D4. Las funciones más comunes

```bash
tail -n +2 results/tabla_genes.tsv | cut -f7 | sort | uniq -c | sort -nr | head -n 5
```

**Resultado:**
```text
    548 hypothetical protein
    152 ABC transporter permease
    111 ABC transporter ATP-binding protein
     94 ABC transporter substrate-binding protein
     62 LysR family transcriptional regulator
```

Hay muchos transportadores ABC, algo típico de bacterias del suelo que
aprovechan muchos nutrientes distintos.

### D5. ¿Dónde están los genes de nodulación?

```bash
grep -i "nodulation" results/tabla_genes.tsv | cut -f1 | sort | uniq -c
```

`grep -i` busca sin importar mayúsculas o minúsculas.

**Resultado:**
```text
     13 NC_003037.1
```

Todos los genes anotados como de nodulación están en **pSymA**, el
megaplásmido simbiótico. Con unos pocos comandos de Unix encontraste algo con
significado biológico.

---

## Resumen de comandos

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
