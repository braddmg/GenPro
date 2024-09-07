---
title: "Anotación de genomas"
layout: page
---
## Activar el ambiente Genomics
```yml
conda activate Genomics
```

## Evaluación de la calidad de los reads
Utilizaremos Fastqc que es un programa que sirve para evaluar la calidad de las secuencias.

```yml
#Primero descomprimimos los archivos
gzip -d *.gz
#Debe crear la carpeta 02.fastqc para que el programa se ejecute correctamente
fastqc *.fastq -o ../02.fastqc/
```
Si no funciona el comando reinstale conda con el siguiente comando y vuelva a ejecutar
