---
title: "Control de calidad y ensamblaje de genomas"
layout: post
---
## Actualización de algunos paquetes

Generalmente si no se actualiza da errores posteriores

<main>
<pre><code class="language-css">pip install matplotlib==3.5.1 <br>conda install --force-reinstall java-jdk
</code></pre>
<style>
  *,
*:before,
*:after {
  box-sizing: border-box;
}

pre[class*="language-"] {
  position: relative;
  overflow: auto;

  /* make space  */
  margin: 5px 0;
  padding: 1.75rem 0 1.75rem 1rem;
  border-radius: 10px;
}

pre[class*="language-"] button {
  position: absolute;
  top: 5px;
  right: 5px;

  font-size: 0.9rem;
  padding: 0.15rem;
  background-color: #828282;

  border: ridge 1px #7b7b7c;
  border-radius: 5px;
  text-shadow: #c4c4c4 0 0 2px;
}

pre[class*="language-"] button:hover {
  cursor: pointer;
  background-color: #bcbabb;
}

main {
  display: grid;
  max-width: 600px;
  margin: 20px auto;
}

h1 {
  font-size: 1.3rem;
}
</style>
<script>
  const copyButtonLabel = "Copy Code";

// use a class selector if available
let blocks = document.querySelectorAll("pre");

blocks.forEach((block) => {
  // only add button if browser supports Clipboard API
  if (navigator.clipboard) {
    let button = document.createElement("button");

    button.innerText = copyButtonLabel;
    block.appendChild(button);

    button.addEventListener("click", async () => {
      await copyCode(block, button);
    });
  }
});

async function copyCode(block, button) {
  let code = block.querySelector("code");
  let text = code.innerText;

  await navigator.clipboard.writeText(text);

  // visual feedback that task is completed
  button.innerText = "Code Copied";

  setTimeout(() => {
    button.innerText = copyButtonLabel;
  }, 700);
}
</script>

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
