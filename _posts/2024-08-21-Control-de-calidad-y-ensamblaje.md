---
title: "Control de calidad y ensamblaje"
layout: page
---
## Activar el ambiente Genomics
```yml
Conda activate Genomics
```

## Convertir archivo bam a fastq
Por algún motivo PacBio envía el archivo en fomato BAM, por lo que hay que convertirlo a fastq.

```yml
samtools fastq m64268e_240324_144300.subreads.bam > A208b_PacBio.fastq
```
## Evaluación de la calidad de los reads
Utilizaremos Fastqc que es un programa que sirve para evaluar la calidad de las secuencias. <br> Vamos a utilizar un loop para procesar todas las secuencias en un sólo comando.

```yml
for f in *.fastq; do fastqc "$f" -o ../02.fastqc/; done;
```

Los archivos estarán en su computadora en una ruta similar a "\\wsl.localhost\Ubuntu\home\user\02.fastqc\" reemplace su usuario.

## Control de calidad con fastq
Utiliazremos el parámetro "detect_adapter_per_pe" para detectar si hay residuos de adaptadores de secuenciación y el "- 30" para eliminar secuencias con calidad menor a 30 según el valor de calidad.

```yml
for i in `ls *_1.fastq.gz | sed 's/_1.fastq.gz//'`; do  fastp -i $i\_1.fastq.gz -I $i\_2.fastq.gz --detect_adapter_for_pe -o ../fastp/$i\_1.fq.gz -O ../fastp/$i\_2.fq.gz -h ../fastp/$i\_fastq.html -e 30; done
```
Ubique los nuevos contis con los comandos cd y ls :)

## Ensamblaje de novo con Spades. 
Utilizaremos los parámetros "--only-assembler" para que no haga corrección de errores en los reads y los valores de k= 33 y 55 para que sólo haga el ensaamblaje con esos dos valores. Debe ajustar el valor de m según la memoria RAM de la que disponga. Por ejemplo si su computadora tien 16 entonces coloque 8. 

```yml
../SPAdes/bin/spades.py --isolate --only-assembler -m 8 -1 A208b_1.fq.gz -2 A208b_2.fq.gz -k 33,55 -o ../ASSEMBLY_SPAdes/
```

El ensamblaje queda guardado en la carpeta ASSEMBLY_SPAdes y es un archivo llamado contigs.fa. Búsquelo con los comandos cd y ls :)
#Renombre el archivo contigs.fa, puede utilizar el nombre A208b.fasta (pista, utilice el comando mv)

## Utilizaremos Quast para visualizar las métricas del ensamblaje de calidad del ensamblaje

```yml
quast.py 208b.fasta -o ../QUAST
```
Si han llegado hasta acá, estoy muy orgulloso!
## Filtrado de contigs
Ahora utilizaremos un comando del software bbtoools para eliminar los contigs menoresa 1000pb.

```yml
reformat.sh in=A208b.fasta out=A208b_filtered.fasta minlength=1000; done
```

## Evaluación de contaminación
Finalmente utilizaremos checkm2 para evaluar la presencia de contaminación

```yml
checkm2 predict --threads 16 --input A208b_filtered.fasta --output-directory ../checkm2
```

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





