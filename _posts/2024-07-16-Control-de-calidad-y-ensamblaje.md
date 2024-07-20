---
title: "Control de calidad y ensamblaje de genomas"
layout: post
---
## Actualización de algunos paquetes

Generalmente si no se actualiza da errores posteriores

<pre id="codecell3" tabindex="0"><code class="language-css">pip install matplotlib==3.5.1 <br>conda install --force-reinstall java-jdk
</code></pre>
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
<button class="copybtn o-tooltip--left" data-tooltip="Copy" data-clipboard-target="#codecell3">
      <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-copy" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#000000" fill="none" stroke-linecap="round" stroke-linejoin="round">
  <title>Copy to clipboard</title>
  <path stroke="none" d="M0 0h24v24H0z" fill="none"></path>
  <rect x="8" y="8" width="12" height="12" rx="2"></rect>
  <path d="M16 8v-2a2 2 0 0 0 -2 -2h-8a2 2 0 0 0 -2 2v8a2 2 0 0 0 2 2h2"></path>
</svg>
    </button> 
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
