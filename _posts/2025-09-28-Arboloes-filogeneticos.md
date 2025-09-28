---
title: "Creación de árboles filogenéticos"
layout: page
---

# Configuración preliminar

```yml
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```
# Descargue los datos e instale el ambiente
```yml
gdown --folder https://drive.google.com/drive/folders/1Sk4rzPMWpA5nLGr1bwt4JOB2yKQUKfd0
conda env create -f env-bayes.yml # Creará un ambiente usando información del archivo descargado.
conda activate bayes-tree
```

# Alinear la secuencia con mafft
```yml
mafft --auto --thread 8 secuencias2.fasta > secuencias.aln.fasta
ls -lh
```
# Cortar con trimal
```yml
trimal -automated1 -terminalonly -in secuencias.aln.fasta -out secuencias.trim.fasta
```
# Una opción para seleccionar el modelo
```yml
modeltest-ng --help
modeltest-ng -i secuencias.trim.fasta -d nt -p 8 -T mrbayes -o secuencias.modeltest
```
Note que no hay una opción de modelo para iqtree, pero se podría usar el mejor modelo encontrado en algún otro programa.
# Usar iqtree para generar el árbol
De igual forma, iqtree permite una opción para seleccionar el modelo en automático
```yml
iqtree -s secuencias.trim.fasta -m MFP -bb 1000 -nt AUTO
```
Visualice el árbol en https://itol.embl.de
