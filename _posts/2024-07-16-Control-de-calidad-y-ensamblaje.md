---
title: "Control de calidad y ensamblaje de genomas"
layout: page
---

## Actualización de algunos paquetes
<div> 
<article>
Se asume que se tiene instalado y actualizado Linux en su computadora. <br>
El siguiente comando actualiza dos paquetes complementarios que pueden dar problemas en comandos posteriores.
</article>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    position: relative;
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    margin-right: 10px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
  }
</style>
</head>
<body>

<div class="container">
  <div class="fixed-text" id="myText">pip install matplotlib==3.5.1 <br>conda install --force-reinstall java-jdk</div>
  <button class="copy-button" id="copyButton" onclick="copyText()">Copiar</button>
</div>

<script>
function copyText() {
  var copyText = document.getElementById("myText");
  var textArea = document.createElement("textarea");
  textArea.value = copyText.textContent;
  document.body.appendChild(textArea);
  textArea.select();
  document.execCommand("copy");
  document.body.removeChild(textArea);

  var copyButton = document.getElementById("copyButton");
  copyButton.textContent = "Copiado";
  
  // Opcionalmente, puedes volver a cambiar el texto después de un tiempo
  setTimeout(function() {
    copyButton.textContent = "Copiar";
  }, 2000); // Cambia el texto a "Copiar" después de 2 segundos (2000 milisegundos)
}
</script>

</body>
</html>

</div>
## Instalación Conda

```yaml
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

## Instalación Spades

```yaml
wget https://github.com/ablab/spades/releases/download/v4.0.0/SPAdes-4.0.0-Linux.tar.gz
tar -xzf SPAdes-4.0.0-Linux.tar.gz
mv SPAdes-4.0.0-Linux SPAdes
Rm SPAdes-4.0.0-Linux.tar.gz
```

## Instalar múltiples paquetes mediante conda.

```yaml
conda install -y -c conda-forge -c bioconda -c AgBiome python=3.10 spades prokka fastqc bbtools trimmomatic quast
wget -nc -i data.txt
gzip -d *.gz
rm data.txt
```
## Fastqc 
Fastqc es un programa que sirve para evaluar la calidad de las secuencias. Vamos a utilizar un loop para procesar todas las secuencias en un sólo comando.

```yaml
for f in *.fastq; do fastqc "$f" -o ../02.fastqc/; done;
```

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
