---
title: "Control de calidad y ensamblaje de genomas"
layout: page
---

## Actualización de algunos paquetes
<div> 
<article>
Se asume que se tiene instalado y actualizado Linux en su computadora. De no ser así, diríjase al siguiente link e instalelo siguiendo las instrucciones: <a href="https://learn.microsoft.com/es-es/windows/wsl/install">Instalar Linux en Windowws </a> <br>
## Actualiazción de paquetes
El siguiente comando actualiza dos paquetes complementarios que pueden dar problemas en comandos posteriores.
</article>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    align-items: center;
    gap: 10px; /* Espacio entre el texto y el botón */
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
    /* Alineación vertical */
    display: flex;
    align-items: center;
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
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    align-items: center;
    gap: 10px; /* Espacio entre el texto y el botón */
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
</style>
</head>
<body>

<div class="container">
  <div class="fixed-text" id="myText">mkdir -p ~/miniconda3 <br>
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh <br>
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3 <br>
rm -rf ~/miniconda3/miniconda.sh <br>
~/miniconda3/bin/conda init bash <br>
~/miniconda3/bin/conda init zsh</div> <br>
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

## Instalación Spades
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    align-items: center;
    gap: 10px; /* Espacio entre el texto y el botón */
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
</style>
</head>
<body>

<div class="container">
  <div class="fixed-text" id="myText">wget https://github.com/ablab/spades/releases/download/v4.0.0/SPAdes-4.0.0-Linux.tar.gz <br>
tar -xzf SPAdes-4.0.0-Linux.tar.gz <br>
mv SPAdes-4.0.0-Linux SPAdes <br>
Rm SPAdes-4.0.0-Linux.tar.gz <br>
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

## Instalar múltiples paquetes mediante conda.
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    align-items: center;
    gap: 10px; /* Espacio entre el texto y el botón */
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
</style>
</head>
<body>

<div class="container">
  <div class="fixed-text" id="myText">conda install -y -c conda-forge -c bioconda -c AgBiome python=3.10 spades prokka fastqc bbtools trimmomatic quast <br>
wget -nc -i data.txt <br>
gzip -d *.gz <br>
rm data.txt <br>
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

## Fastqc 
Fastqc es un programa que sirve para evaluar la calidad de las secuencias. Vamos a utilizar un loop para procesar todas las secuencias en un sólo comando.
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Copiar Texto</title>
<style>
  .container {
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    display: flex;
    align-items: center;
    gap: 10px; /* Espacio entre el texto y el botón */
  }
  .copy-button {
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
  .fixed-text {
    flex: 1;
    padding: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 3px;
    user-select: all; /* Permite seleccionar el texto */
    color: blue; /* Color del texto azul */
    /* Alineación vertical */
    display: flex;
    align-items: center;
  }
</style>
</head>
<body>

<div class="container">
  <div class="fixed-text" id="myText">for f in *.fastq; do fastqc "$f" -o ../02.fastqc/; done;
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


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
