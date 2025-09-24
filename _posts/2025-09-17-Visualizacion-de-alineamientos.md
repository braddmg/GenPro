---
title: "Visualización de alineamientos"
layout: page
---

## Descargue los datos e instale los paquetes

```yml
pip install gdown # Instalará una herramienta que permite descargar archivos desde google drive
gdown --folder https://drive.google.com/drive/folders/1Sk4rzPMWpA5nLGr1bwt4JOB2yKQUKfd0
cd clase_alineamientos # El comando "cd" le permite moverse de un directorio (carpeta) a otro. Debe poner la dirección del nuevo directorio.
```

# Remover el ambiente de conda instalado previamente
```yml
conda remove -n pymsaviz --all -y
```
# Instalar nuevamente
Instalar la herramienta a utilizar, la documentación está disponible [aquí](https://moshi4.github.io/pyMSAviz/getting_started). 
```yml
conda create -n pymsaviz -c conda-forge -c bioconda pymsaviz -y 
conda activate pymsaviz
python
```
Al Ejecucutar el comando "python" se le abrirá un tipo de nueva interfaz dónde los códigos que ejecutemos deben ser de python. 
Los siguientes comando crearan figuras de alineamiento.

## Visualización con el paquete pymsaviz
```yml
from pymsaviz import MsaViz # En python hay que especificar qué funciones queremos importar. En esta caso sólo utilizaremos la función MsaViz de la librería pymsaviz
msa= "aligned.fas" # Generamos un objeto llamado msa, que contiene el archivo fasta con las secuencias alineadas.
mv = MsaViz(msa, format="fasta") # mv es un nuevo objeto que va a guardar el resultado de la función "MsaViz" que contiene toda la información necesaria para la visualización
mv.savefig("plot.png") # el ".savefig" indica que guardemos la figura que está dentro del archivo que creameos previamente llamado "mv". En los paréntesis y en comillas pueden poner el nombre que quieran ponerle
```
Nueva versión del gráfico
```yml
mv2 = MsaViz(msa, wrap_length=60, show_grid=True, show_consensus=True, format="fasta")
mv2.savefig("plot2.png")
```
Otra versión
```yml
mv3 = MsaViz(msa, wrap_length=60, color_scheme="Flower", show_count=True, start=370, end=760, show_seq_char=False, show_consensus=True, consensus_color="tomato", format="fasta")
mv3.savefig("plot3.png")
```
Vamos a añadir una marca en la mutación encontrada

```yml
mv3.add_markers([555], color="red", marker="x") # la posición dónde está la mutación es la 555 de la secuencia de ref.
mv3.savefig("plot_with_mark.png") # Guarda el nuevo plot con el nombre, plot with mark
```

## Otro ejemplo con proteínas FIC
Estas proteínas son sacadas de [este artículo](https://academic.oup.com/femsle/article/doi/10.1093/femsle/fnaf092/8244153#531429867)  en dónde estudiamos los plásmidos de *H. pylori*. Son proteínas relacionadas con patogenicidad pero también con sistemas toxina-antitoxina. Todas deberían tener el "motif" *HxFx(D/E)GNGRxxR*
```yml
msa= "fic_aligned.fas"
mv = MsaViz(msa, wrap_length=50, color_scheme="Flower", show_count=True, show_seq_char=True, show_consensus=True, consensus_color="tomato", start=540, format="fasta")
mv.add_text_annotation((709, 720), "Adenylytation motif", text_color="red", range_color="red")
mv.savefig("Fic_plot.png")

```

## Tarea
Busque al menos 3 (pueden ser más) secuencias de algún gen de interés en diferentes especies y anote alguna de las mutaciones y gaps (indels) encontrados. 
Debe dar una breve introducción del gen utilizado.
