---
title: "Preparación ambiente Linux"
layout: page
---

## Instalación Conda
<article>
Se asume que se tiene instalado y actualizado Linux en su computadora. De no ser así, diríjase al siguiente link e instalelo siguiendo las instrucciones: <a href="https://learn.microsoft.com/es-es/windows/wsl/install">Instalar Linux en Windowws </a> <br>
Conda es un programa que crea un ambiente en Linux dónde podemos cargar diferentes paquetes automáticamente y para diferentes aplicaciones
</article>

```yml
#Crear directorio
mkdir -p ~/miniconda3
#Descargar archivos
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
#Instalar miniconda
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```
## Si tiene MAC use el siguiente comando
```yml
mkdir -p ~/miniconda3
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
```
Cierra y vuelva a abrir la terminal

## Actualización de algunos paquetes

El siguiente comando actualiza dos paquetes complementarios que pueden dar problemas en comandos posteriores.

```yml
pip install -U matplotlib
conda install --force-reinstall java-jdk
```
#Crear ambientes a utilizar
```yml
#ambiente para ejecutar fastqc
conda create -c bioconda -c conda-forge fastqc -n fastqc
#Ambiente para fastp y spades
conda create -n Genomics
#Instalar paquetes en el ambiente
conda install -y -c conda-forge -c bioconda -c AgBiome python=3.10 spades fastp -n Genomics
# Instalar otros ambientes
conda create -c bioconda -c conda-forge quast -n quast
conda create -c conda-forge -c bioconda -c defaults prokka -n prokka
```
# Para MAC

```yml
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
conda create -n fastqc
conda activate fastqc
brew install fastqc
conda create -n Genomics
#Instalar paquetes en el ambiente
conda install -y -c conda-forge -c bioconda -c AgBiome python=3.10 fastp -n Genomics
conda install y -c conda-forge -c bioconda -c AgBiome python=3.10 spades -n Genomics
```
## Descargar los datos
```yml
#cree una carpeta llamada clas, dónde ejecutaremos todo
mkdir clase
#Muévase a la carpeta con el comando cd
cd clase/
#Descargue los datos a utilizar
pip install gdown
gdown --folder 104Tl8ou0AFPWXpn5BII_3H9a7BJeXGgU?usp=sharing 
mv Data 01.Data
cd 01.Data
```
Si tiene MAC debe descargarlos manualmente con el siguiente link de [google drive](https://drive.google.com/drive/folders/104Tl8ou0AFPWXpn5BII_3H9a7BJeXGgU?usp=sharing
)
