---
title: "Control de calidad y ensamblaje"
layout: page
---

## Evaluación de la calidad de los reads
Utilizaremos Fastqc que es un programa que sirve para evaluar la calidad de las secuencias.

```yml
#Activamos el ambiente fastqc
conda activate fastqc
#Debe crear la carpeta fastqc_results para que el programa se ejecute correctamente
fastqc *.fastq -o .fastqc_results
```
Los archivos estarán en su computadora en una ruta similar a "\\wsl.localhost\Ubuntu\home\user\Data\fastqc_results\" reemplace su usuario. Abra el archivo en formato html

## Control de calidad con fastp
Utiliazremos el parámetro "detect_adapter_per_pe" para detectar si hay residuos de adaptadores de secuenciación y el "- 30" para eliminar secuencias con calidad menor a 30 según el valor de calidad. Cree la carpeta fastp en el home antes de ejecutar el comando. 

```yml
conda deactivate
conda activate Genomics
for i in `ls *_1.fastq | sed 's/_1.fastq//'`; do  fastp -i $i\_1.fastq -I $i\_2.fastq --detect_adapter_for_pe -o ../fastp/$i\_1.fq.gz -O ../fastp/$i\_2.fq.gz -h ../fastp/$i\_fastq.html -e 30; done
```
Ubique los nuevos contis con los comandos cd y ls :)

## Ensamblaje de novo con Spades. 
Utilizaremos los parámetros "--only-assembler" para que no haga corrección de errores en los reads y los valores de k= 33 y 55 para que sólo haga el ensaamblaje con esos dos valores. Debe ajustar el valor de m según la memoria RAM de la que disponga. Por ejemplo si su computadora tien 16 entonces coloque 8. 

```yml
#Instalemos nuevamente SPAdes pero ahora desde conda
conda install -c bioconda spades -n Genomics
spades.py --isolate -m 8 -1 A208b_1.fq.gz -2 A208b_2.fq.gz -k 33,55 -o ../ASSEMBLY_SPAdes/
```

El ensamblaje queda guardado en la carpeta ASSEMBLY_SPAdes y es un archivo llamado contigs.fa. Búsquelo con los comandos cd y ls :)
Renombre el archivo contigs.fa, puede utilizar el nombre A208b.fasta (pista, utilice el comando mv)

## Utilizaremos Quast para visualizar las métricas del ensamblaje de calidad del ensamblaje

```yml
quast.py A208b.fasta -o ../QUAST/A208b
```
Si han llegado hasta acá, estoy muy orgulloso!
## Filtrado de contigs
Ahora utilizaremos un comando del software bbtoools para eliminar los contigs menores a 1000pb.

```yml
#Instalar seqtk
conda install bioconda::seqtk -n Genomics
seqtk seq -L 1000 A208b.fasta > A208b_filtered.fasta
```
Vuelva a revisar el nuevo archivo con Quast

## Uso del Kabré
Muy bien! Ahora intentemos hacerlo en el servidor del CENAT
Abra windows powershell en su computadora (no es necerio que sea wsl) o la aplicación MobaXterm
Ejecute el siguiente comando reemplazando su usuario. Automáticamente se le solicitará su contraseña y al digitarla no aparecerá en la pantalla por una cuestión de seguridad. Cuando termine presione enter.

```yml
ssh user@cluster.cenat.ac.cr
```
Utilice el siguiente comando para copiar los datos a su carpeta 
```yml
cp /work/bmendoza/ejemplo ejemplo
```

## Convertir archivo bam a fastq
Por algún motivo PacBio envía el archivo en fomato BAM, por lo que hay que convertirlo a fastq.
Revise que se haya creado la carpeta "ejemplo" y muévase dentro de ella.
```yml
#Convertiremos el archivo bam a fastq
samtools fastq m64268e_240324_144300.subreads.bam > A208b_PacBio.fastq
```

## Visualización de archivos .slurm
En su carpeta hay varios archivos en formato slurm. Estos los utilizaremos para enviar trabajos remotos de cada programa.
Ejecute el primer archivo llamado fastp.slurm
```yml
cat fastp
sbatch fastp.slurm
#Podemos revisar el proceso de nuestro trabajo con el siguiente comando:
squeue
```
Una vez termine nuestro trabajo, podemos abrir el archivo fastp.txt con el comando cat. Este contiene los resultados.

## Ensamblaje híbrido
Revise el archivo llamado SPAdes.slurm. Entiéndalo antes de enviarlo.
```yml
cat SPAdes.slurm
sbatch SPAdes.slurm
squeue
```

## Evaluación de la calidad con Quast

```yml
sbatch quast.slurm
```

## Evaluación de contaminación
Finalmente utilizaremos checkm2 para evaluar la presencia de contaminación en la muestra. 

```yml
cat checkm2.slurm
sbatch checkm2.slurm
squeue
cat checkm2.txt
```



