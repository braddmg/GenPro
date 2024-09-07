---
title: "Anotación de genomas"
layout: page
---
## copiaremos los archivos a utilizar
```yml
cp /work/bmendoza/*.slurm
#Qué significa el *.slurm?
```

## Utilizaremos Prokka para ensamblar!
Utilizaremos Fastqc que es un programa que sirve para evaluar la calidad de las secuencias.

```yml
#Primero descomprimimos los archivos
gzip -d *.gz
#Debe crear la carpeta 02.fastqc para que el programa se ejecute correctamente
fastqc *.fastq -o ../02.fastqc/
```
Si no funciona el comando reinstale conda con el siguiente comando y vuelva a ejecutar
