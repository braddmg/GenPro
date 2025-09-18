---
title: "Visualización de alineamientos"
layout: page
---

## Descargue los datos

```yml
pip install gdown # Instalará una herramienta que permite descargar archivos desde google drive
gdown --folder  
cd clase_alineamientos # El comando "cd" le permite moverse de un directorio (carpeta) a otro. Debe poner la dirección del nuevo directorio.

```

Instalar la herramienta a utilizar, la documentación está disponible aquí https://moshi4.github.io/pyMSAviz/getting_started
```yml
conda create -n pymsaviz -c conda-forge -c bioconda pymsaviz -y 
conda activate pymsaviz
python
```
Al Ejecucutar el comando "python" se le abrirá un tipo de nueva interfaz dónde los códigos que ejecutemos deben ser de python. 
Los siguientes comando crearan figuras de alineamiento.

```yml
from pymsaviz import MsaViz # En python hay que especificar qué funciones queremos importar. En esta caso sólo utilizaremos la función MsaViz de la librería pymsaviz
msa= "aligned.fas" # Generamos un objeto llamado msa, que contiene el archivo fasta con las secuencias alineadas.
mv = MsaViz(msa) # mv es un nuevo objeto que va a guardar el resultado de la función "MsaViz" que contiene toda la información necesaria para la visualización
mv.savefig("plot.png") # el ".savefig" indica que guardemos la figura que está dentro del archivo que creameos previamente llamado "mv". En los paréntesis y en comillas pueden poner el nombre que quieran ponerle
```
Nueva versión del gráfico
```yml
mv2 = MsaViz(msa, wrap_length=60, show_grid=True, show_consensus=True)
mv2.savefig("plot2.png")
```
Otra versión
```yml
mv3 = MsaViz(msa_file, wrap_length=60, color_scheme="Flower", show_count=True, start=100, end=160, show_seq_char=False, show_consensus=True, consensus_color="tomato")
mv4.savefig("plot3.png")
```

