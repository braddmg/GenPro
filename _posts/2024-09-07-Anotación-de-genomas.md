---
title: "Anotación de genomas"
layout: page
---
## Conectarse al servidor Kabré
A partir de ahora trabajaremos en el clúster computacional del CENAT.
```yml
#Para conectarse reemplace su usuario
user@cluster.cenat.ac.cr
#Digite su contraseña
```
## Copiaremos los archivos a utilizar
```yml
cp /work/bmendoza/CURSO/annot.slurm annot.slurm
cp /work/bmendoza/CURSO/A231_12.fasta A231_12.fasta
```

## Anotación con múltiples herramientas 
Vamos a utilizar diferentes herramientas vistas en la primera mitad de la clase. Es bueno que sepan que hay muchos recursos disponibles y que es recomendado anotar con varias para comparar. Vamos a trabajar con un sólo slurm, ábralo y entiéndalo. Consulte si tiene dudas. 
```yml
cat annot.slurm
#El archivo es el siguiente:

#!/bin/bash
#SBATCH --job-name=Anotacion
#SBATCH --output=anotacion.txt
#SBATCH --partition=dribe
#SBATCH --ntasks=8
#SBATCH --time=72:00:00

module load miniconda/eggnog-mapper-2.1.6
module load miniconda/abricate
module load miniconda/mob-suite-3.1.7
module load miniconda/checkm2
module load quast/5.2.1
module load seqtk

cp ASSEMBLY/contigs.fasta A208b.fasta

seqtk seq -L 1000 A208b.fasta > A208b_F.fasta
quast.py A208b_F.fasta -o QUAST/A208b
checkm2 predict --threads 8 --input A208b_F.fasta --output-directory checkm2
abricate A231_12.fasta --db ncbi > abricate.tsv
mob_recon --infile A231_12.fasta --outdir mobsuite/ -c

module purge

module load prokka/1.14.6

prokka --prefix A208b --outdir Prokka A208b_F.fasta --cpu 8

module purge

module load miniconda/eggnog-mapper-2.1.6

mkdir eggnog

emapper.py -m diamond --itype genome -i A208b_F.fasta --output_dir eggnog/ --cpu 8 -o A208b
```
## Envíe el slurm a la cola
Utilice el comando aprendido en la clase anterior para enviar el slurm a la cola. Es importante que el archivo slurm esté en su carpeta de home. Para verificar esto puede usar el comando pwd.
Una veez finalice, explore los archivos generados. Muévase en las carpetas y descargue el archivo con de las secuencias de nuleótidos y de aminoácidos.

## Descargar archivos sin moba
Para esto debe abrir una nueva pestaña del powershell o terminal, o bien salir del cluster con el comando exit.
```yml
#Cerrar sesión en el servidor
exit
#Copiar archivos de su usuario a su computadora. En mi caso lo copiaré a la carpeta Documents
scp -r user@cluster.cenat.ac.cr:/home/A208b_F.fasta C:\Users\suusuario\Documents
#Repita el mismo comando pero para descargar el archivo A208b.faa
```
