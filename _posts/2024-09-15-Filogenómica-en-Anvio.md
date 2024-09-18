---
title: "Filogenómica"
layout: page
---
## Conectarse al servidor Kabré
A partir de ahora trabajaremos en el clúster computacional del CENAT.
```yml
#Para conectarse reemplace su usuario
user@cluster.cenat.ac.cr
#Digite su contraseña
```
## Verifique cuanto espacio tiene usado el cluster y cuánto le queda disponible. 
Necesitaremos por lo menos 6gb libres para poder correr los análisis
```yml
df -h /home/user
```
Si no tiene 6gb libres puede borrar los archivos anterior que hemos usado con el comando rm -r *
## Copiaremos los archivos a utilizar
```yml
cp /work/bmendoza/CURSO/anvio/Agrobacterium/anvio.slurm anvio.slurm
cp /work/bmendoza/CURSO/anvio/Agrobacterium/pan.slurm pan.slurm
cp /work/bmendoza/CURSO/anvio/Agrobacterium/taxonomy.slurm taxonomy.slurm
cp /work/bmendoza/CURSO/anvio/Agrobacterium/drep.slurm drep.slurm
cp -r /work/bmendoza/CURSO/anvio/Agrobacterium/Agro Agro
cp -r /work/bmendoza/CURSO/anvio/Agrobacterium/Agro-GENOMES.db Agro-GENOMES.db
cp -r /work/bmendoza/CURSO/anvio/Agrobacterium/A208b.db A208b.db
mkdir fasta
cp -r /work/bmendoza/CURSO/anvio/Agrobacterium/fasta/*.fasta fasta

```

## Anotación con múltiples herramientas 
El archivo anvio.slurm usa los archivos fasta para crear las bases de datos de anvio.
En su caso ya les di los archivos .db para no tener que generarlos nuevamente.
El archivo pan.slurm genera el análisis pangenómico inicial. También les pase la base de datos del pangenoma pero igual vamos a dejar corriendo varios comandos.
```yml
#veamos el arcihvo pan.slurm
cat pan.slurm
module load miniconda/anvio-7.1

#anvi-gen-genomes-storage -e external-genomes.txt \
                         -o Agro-GENOMES.db

#anvi-pan-genome -g Agro-GENOMES.db \
                --project-name Agro \
                --num-threads 32

anvi-get-sequences-for-gene-clusters -g Agro-GENOMES.db -p Agro/Agro-PAN.db -o genesDNA.fasta \
--max-num-genes-from-each-genome 1 --min-num-genomes-gene-cluster-occurs 41 --report-DNA-sequences \
--concatenate-gene-clusters

module unload miniconda/anvio-7.1

module load  mafft/7.397

mafft --retree 1 --maxiterate 0 genesDNA.fasta > out.aln

module unload mafft/7.397
module load fasttree/2.1.10

FastTree -gtr -nt < out.aln > tree_file
```
Si analizamos el archivo, los primeros comandos tienen un # antes, esto hace que el comando no se ejcute.
Luego aislamos los genes que estén una única vez en todos los genomas (core genome) en un nuevo archivo.
Ese archivo con todos los genes concatenados lo alineamos con maft y finalmente generamos el árbol con fasttree. 

## Taxonomía del aislamiento A208b según anvio
Anvio nos permite conocer la taxonomía de un genoma
```yml
cat taxonomy.slurm
anvi-run-scg-taxonomy -c A208b.db --debug
anvi-estimate-scg-taxonomy -c A208b.db --debug
```
Analice los resultados que se encuentran en el archivo tax.txt

## Distancias de MASH 
Vamos a usar un software que se llama dRep para realizar dendogramas basados en las distancias de MASH y determinar si hay genomas con más de un 95% de diferencia en el ANI.
```yml
cat drep.slurm
dRep compare drep -g *.fa -pa 0.95 -sa 0.97
```
Descargue los resultados que están en la carpeta drep
