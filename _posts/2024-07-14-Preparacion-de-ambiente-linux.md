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

## Descargar los datos
```yml
pip install gdown
gdown --folder 104Tl8ou0AFPWXpn5BII_3H9a7BJeXGgU?usp=sharing 
cd /Data
gzip -d *.gz
```
