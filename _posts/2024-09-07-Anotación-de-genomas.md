---
title: "Anotación de genomas"
layout: page
---
## Copiaremos los archivos a utilizar
```yml
cp /work/bmendoza/anotacion.slurm anotacion.slurm
cp /work/bmendoza/A231_12.fasta
```

## Anotación con múltiples herramientas 
Vamos a utilizar diferentes herramientas vistas en la primera mitad de la clase. Es bueno que sepan que hay muchos recursos disponibles y que siempre es muy anotar con varias para comparar. Somo vamos a trabajar con un sólo slurm, ábralo y entiéndalo. Consulte si tiene dudas. 
```yml
cat anotacion.slurm
sbatch anotacion.slurm
```
Explore los archivos generados. Muévase en las carpetas y descargue el archivo con de las secuencias de nuleótidos y de aminoácidos.
## Descargar archivos sin moba
Para esto debe abrir una nueva pestaña del powershell o terminal, o bien salir del cluster con el comando exit.
```yml
#Cerrar sesión en el servidor
exit
#Copiar archivos de su usuario a su computadora. En mi caso lo copiaré a la carpeta Documents
scp -r user@cluster.cenat.ac.cr:/home/A208b_F.fasta C:\Users\suusuario\Documents
#Repita el mismo comando pero para descargar el archivo A208b.faa
```
