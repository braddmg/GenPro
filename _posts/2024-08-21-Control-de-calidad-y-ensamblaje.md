---
title: "Control de calidad y ensamblaje"
layout: page
---

## Evaluación de la calidad de los reads
Utilizaremos Fastqc que es un programa que sirve para evaluar la calidad de las secuencias.

```yml
#Activamos el ambiente fastqc
conda activate fastqc
#Debe crear la carpeta 02.fastqc para que el programa se ejecute correctamente
mkdir ../02.fastqc
fastqc *.fastq.gz -o ../02.fastqc
```
Los archivos estarán en su computadora en una ruta similar a "\\wsl.localhost\Ubuntu\home\user\Data\fastqc_results\" reemplace su usuario. Abra el archivo en formato html

## Control de calidad con fastp
Utiliazremos el parámetro "detect_adapter_per_pe" para detectar si hay residuos de adaptadores de secuenciación y el "- 30" para eliminar secuencias con calidad menor a 30 según el valor de calidad. Cree la carpeta fastp en el home antes de ejecutar el comando. 

```yml
#Debe crear la carpeta "../03.fastp", inténtelo. 
conda deactivate
conda activate Genomics
for i in `ls *_1.fastq.gz | sed 's/_1.fastq.gz//'`; do  fastp -i $i\_1.fastq.gz -I $i\_2.fastq.gz --detect_adapter_for_pe -o ../03.fastp/$i\_1.fq.gz -O ../03.fastp/$i\_2.fq.gz -h ../03.fastp/$i\_fastq.html -e 30; done
```
Ubique los nuevos contis con los comandos cd y ls :)

## Ensamblaje de novo con Spades. 
Utilizaremos los parámetros "--only-assembler" para que no haga corrección de errores en los reads y los valores de k= 33 y 55 para que sólo haga el ensaamblaje con esos dos valores. Debe ajustar el valor de m según la memoria RAM de la que disponga. Por ejemplo si su computadora tien 16 entonces coloque 14, deje unos 2gb para que no muera. 

```yml
# muévase a la carpeta dónde están los resultados de fastp.
#Ejecute el siguiente comando para el ensamblaje.
spades.py --isolate -m 14 -1 ../03.fastp/A208b_1.fq.gz -2 ../03.fastp/A208b_2.fq.gz -k 33,55 -o ../04.ASSEMBLY_SPAdes/
```

El ensamblaje queda guardado en la carpeta ASSEMBLY_SPAdes y es un archivo llamado contigs.fa. Búsquelo con los comandos cd y ls :)
Renombre el archivo contigs.fa, puede utilizar el nombre A208b.fasta (pista, utilice el comando mv)

## Utilizaremos Quast para visualizar las métricas de calidad del ensamblaje

```yml
conda deactivate
conda activate quast
quast.py A208b.fasta -o ../QUAST/A208b
```
Si han llegado hasta acá, estoy muy orgulloso!

# Anotación con Prokka
Utilizaremos Prokka para ver los genes anotados
```yml
conda deactivate
conda activate prokka
prokka --outdir ../06.Prokka --prefix A208b A208b.fasta
```
#Si tiene MAC
```yml
conda create -n prokka
conda deactivate
conda activate prokka
brew install brewsci/bio/prokka
prokka --outdir ../06.Prokka --prefix A208b A208b.fasta
```
# Phylogenomics made easy
Vamos a ejecutar GenFlow, que nos da como output un árbol filogenómico con un sólo comando. Sorry, no lo he estandarizado para MAC :(
```yml
#Descargue el repositorio del github
cd #esto los devuelve al home
git clone https://github.com/braddmg/GenFlow.git
#Muévase a la nueva carpeta
cd GenFlow
#Crear un nuevo ambiente utilizando un archivo de configuración
conda env create -f GenFlow.yml
conda deactivate
conda activate GenFlow
#Ejecutar la configuración del script
bash setup.sh
#Reinicie el ambiente y pruebe que todo funcione con el comando GenFlow
conda deactivate
conda activate GenFlow
GenFlow -h
```
Si se muestra el mensaje de help, entonces la instalación funcionó sin problemas.
En la carpeta 01.Data hay un archivo que se llama "references.txt" este tiene una lista de códigos que usaremos como genomas de referencia.
```yml
#Cree una nueva carpeta
cd
mkdir 07.Phylogenomics
#Mueva el archivo con la lista de genomas
mv 01.Data/references.txt 07.Phylogenomics/
#Mueva su genoma a la misma carpeta
mv 04.ASSEMBLY_SPAdes/A208b.fasta 07.Phylogenomics/
cd 07.Phylogenomics/
```
Una vez dentro de la carpeta 07.Phylogenomics revise si ya tiene los archivos (el fasta y el txt) con el comando ls. Y ejecute el comando GenFlow.
```yml
GenFlow -g references.txt -f A208b.fasta -t 12 -G 0.8 -F 0.8
cd results/
ls
```
En la carpeta results, debe tener un archivo .tree y varios archivos .svg que son los heatmap con los valores de ANI.
El archivo .tree puede visualizarlo en la página de [iTOL](https://itol.embl.de).

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



