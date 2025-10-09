---
title: "Anotación de genomas"
layout: page
---
## Preparación de datos y carpetas
```yml
gdown --folder https://drive.google.com/drive/folders/1KZYKmDkXK9f7bbLpRqFTSHbTm5VyFkMI?usp=sharing
cd clase_anotacion
mkdir -p results/prokka results/hmmer results/amrfinder logs
```
## Instalar herramientas en un sólo ambiente (windows)
```yml
conda create -y -n annotation -c conda-forge -c bioconda -c defaults \
  prokka hmmer ncbi-amrfinderplus
# Activar ambiente
conda activate annotation
```
## Instalar herramientas en un sólo ambiente (MAC)
```yml
conda create -y -n annotation -c conda-forge -c bioconda ncbi-amrfinderplus
# Activar ambiente
conda activate annotation
# Instalar
brew install brewsci/bio/prokka
brew install hmmer
```

## Descagar amrfinder database
Puede tardar un rato
```yml
amrfinder -u
```
## Anotación con prokka
```yml
prokka data/INISA09.fna \
  --outdir results/prokka \
  --prefix genome \
  --cpus 8 \
  --force \
  2> logs/prokka.stderr
```
## Anotación de genes esenciales con hmmer
```yml
cd db
unzip bacterial_129_PFAM.hmm.zip
cd ../
hmmpress db/bacterial_129_PFAM.hmm
hmmsearch \
  --cpu 8 \
  --tblout results/hmmer/custom.tbl \
  --domtblout results/hmmer/custom.domtbl \
  db/bacterial_129_PFAM.hmm \
  data/INISA09.faa
```

## Anotación de genes de resistencia
```yml
amrfinder \
  -n data/INISA09.fna \
  --threads 8 \
  --plus \
  -o results/amrfinder/amrfinder_nucl.tsv  
```
