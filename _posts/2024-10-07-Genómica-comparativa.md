---
title: "Genómica comparatia"
layout: page
---
## Visualización
Vamos a jugar un poco más con la visualización!! Entonces vayan de nuevo a la carpeta Prochlorococcus_31_genomes de la clase pasada.<br>
Dentro de esta carpeta (dónde están todos los archivos .db) vamos a ejecutar el siguiente comando.
```yml
anvi-display-pan -g PROCHLORO-GENOMES.db \
                 -p PROCHLORO/Prochlorococcus_Pan-PAN.db
```
## Filtrar el pangenoma

Mediante la interfaz de anvio vamos a generar diferentes bins de secciones importantes del pangenoma. <br>
Usando los filtros de la interfaz seleccionie el core genome y los singletons. Intente hacerlo sólo basado en lo aprendido en la clase anterior.

## Anvio split pangenome
Podemos tomar esos gene clusters que seleccionamos manualmente y separarlos del pangenoma para explorarlos mejor.

```yml
anvi-split -p PROCHLORO/Prochlorococcus_Pan-PAN.db -g PROCHLORO-GENOMES.db -C default -o SPLIT_PANs
```
## Nueva visualización
Dentro de la nueva carpeta creada, que se llama SPLIT_PANs habrá dos archivos, uno llamado Singletons y otro llamado core. <br>
Contienen sólo la sección del pangenoma que seccionamos! Vamos a revisar los Singletnos.

```yml
anvi-display-pan -p SPLIT_PANs/Singletons/PAN.db \
                 -g PROCHLORO-GENOMES.db
```
Aquí podemos visualizar sólo los singletons de cada genoma. <br>
Vamos a extraer los singletons del genoma MIT9515. Y extraemos los genes con el siguiente comando.
```yml
```yml
anvi-get-sequences-for-gene-clusters -g PROCHLORO-GENOMES.db -p SPLIT_PANs/Singletons/PAN.db -o MIT9515.fasta -C default -b MIT9515
head MIT9515.fasta
```
Este es un archivo con las secuencias de aminoácidos de cada gen que se encontraba únicamente en el genoma MIT9515. Puede usarlo para anotar su función con alguna de las herramientas vistas en clase y saber qué funciones tiene su genoma que no tienen los demás con los que compara.

## Extraer los core genes bajo ciertos parámetros
```yml
anvi-get-sequences-for-gene-clusters -g PROCHLORO-GENOMES.db -p PROCHLORO/Prochlorococcus_Pan-PAN.db -o core-sequences.fasta \
                                         --max-num-genes-from-each-genome 1 \
                                         --min-num-genomes-gene-cluster-occurs 31 \
                                         --concatenate-gene-clusters \
                                         --min-geometric-homogeneity-index 0.8 \
                                         --min-functional-homogeneity-index 0.8
```
## Análisis de enriquecimiento funcional
Ejecutemos primero el siguiente comando para instalar una librería en R
```yml
Rscript -e 'install.packages("BiocManager",
              repos="https://cran.rstudio.com"); BiocManager::install("qvalue")'
```
Ahora sí, ejecutemos el análisis funcional para averiguar si hay funciones mayormente presentes en genomas aislados de un ambientes con más o menos luz.
```yml
anvi-compute-functional-enrichment-in-pan -p PROCHLORO/Prochlorococcus_Pan-PAN.db \
                                          -g PROCHLORO-GENOMES.db \
                                          --category light \
                                          --annotation-source COG14_FUNCTION \
                                          -o enriched-functions.txt
```
El archivo enriched-functions.txt tiene la información sobre las funciones que están enriquecidas para ciertos grupo de genomas. <br>
Intente abrirlo en un excel para analizarlo mejor. 

## ANI
En anvio también podemos calcular el ANI de los genomas con la siguiente función.
```yml
anvi-compute-genome-similarity --external-genomes external-genomes.txt --program fastANI --output-dir ANI \
--num-threads 8 --pan-db PROCHLORO/Prochlorococcus_Pan-PAN.db
```
Visualizamos de nuevo!
```yml
anvi-display-pan -g PROCHLORO-GENOMES.db \
                 -p PROCHLORO/Prochlorococcus_Pan-PAN.db
```
