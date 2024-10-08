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
anvi-split -p Prochlorococcus-PAN.db \
           -g Prochlorococcus-GENOMES.db \
           -C default \
           -o SPLIT_PANs
```

## Extraer los core genes
```yml
anvi-get-sequences-for-gene-clusters -g PROCHLORO-GENOMES.db -p PROCHLORO/Prochlorococcus_Pan-PAN.db -o core-sequences.fasta \
                                         --max-num-genes-from-each-genome 1 \
                                         --min-num-genomes-gene-cluster-occurs 31 \
                                         --concatenate-gene-clusters \
                                         --min-geometric-homogeneity-index 0.8 \
                                         --min-functional-homogeneity-index 0.8
```
## Instalación de dependencias
