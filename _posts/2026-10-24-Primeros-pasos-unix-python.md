# Bioinformatics Cheatsheet: Unix & Biopython

Practical, copy-paste examples for everyday bioinformatics work: inspecting
sequence files, wrangling tables, batch processing, downloading data from NCBI,
and scripting with Biopython.

All Unix examples assume **GNU tools** (Linux). On macOS, install `coreutils`,
`gnu-sed` and `gawk` with Homebrew, or adjust flags such as `sed -i`.

## Contents

- [Unix](#unix)
  - [Files and navigation](#files-and-navigation)
  - [Viewing files](#viewing-files)
  - [Compressed files](#compressed-files)
  - [FASTA](#fasta)
  - [FASTQ](#fastq)
  - [grep: searching](#grep-searching)
  - [cut, sort, uniq: tables](#cut-sort-uniq-tables)
  - [awk: column processing](#awk-column-processing)
  - [sed: find and replace](#sed-find-and-replace)
  - [Joining and comparing files](#joining-and-comparing-files)
  - [Loops and batch processing](#loops-and-batch-processing)
  - [Downloading data from NCBI](#downloading-data-from-ncbi)
  - [Common bioinformatics tools](#common-bioinformatics-tools)
  - [HPC and long-running jobs](#hpc-and-long-running-jobs)
- [Biopython](#biopython)
  - [Reading and writing sequences](#reading-and-writing-sequences)
  - [Working with sequences](#working-with-sequences)
  - [GenBank files and features](#genbank-files-and-features)
  - [FASTQ and quality scores](#fastq-and-quality-scores)
  - [NCBI Entrez](#ncbi-entrez)
  - [Pairwise alignment](#pairwise-alignment)
  - [Multiple sequence alignments](#multiple-sequence-alignments)
  - [Phylogenetic trees](#phylogenetic-trees)
  - [Parsing BLAST results](#parsing-blast-results)
- [Regex quick reference](#regex-quick-reference)

---

# Unix

## Files and navigation

```bash
pwd                               # current directory
ls -lh                            # list with human-readable sizes
ls -lhS                           # sort by size (largest first)
ls -lht                           # sort by modification time (newest first)
du -sh *                          # size of each file/folder here
du -sh * | sort -h                # ... sorted by size
df -h .                           # free space on this disk

find . -name "*.fasta"                    # find files by name
find . -name "*.fastq.gz" -size +1G       # ... larger than 1 GB
find . -type f -mtime -7                  # modified in the last 7 days
find . -name "*.tmp" -delete              # find and delete (careful!)

mkdir -p results/{qc,assembly,annotation} # create several folders at once
cp -r data/ backup/                       # copy a folder
mv old_name.txt new_name.txt              # rename / move
ln -s /path/to/big_file.fa .              # symbolic link instead of copying
```

## Viewing files

```bash
head -n 20 file.tsv               # first 20 lines
tail -n 20 file.tsv               # last 20 lines
tail -n +2 file.tsv               # everything except the header
less -S file.tsv                  # scroll without wrapping long lines (q to quit)
wc -l file.tsv                    # number of lines
column -t -s $'\t' file.tsv | less -S          # pretty-print a TSV
head -1 file.tsv | tr '\t' '\n' | cat -n       # numbered list of column names
```

## Compressed files

```bash
gzip file.fastq                   # compress   -> file.fastq.gz
gunzip file.fastq.gz              # decompress -> file.fastq
gzip -k file.fastq                # compress but keep the original
zcat file.fastq.gz | head         # view without decompressing
zgrep -c "^>" seqs.fa.gz          # grep inside a .gz
zless file.fastq.gz

tar -czvf archive.tar.gz folder/  # create a tar.gz
tar -xzvf archive.tar.gz          # extract a tar.gz
tar -tzvf archive.tar.gz          # list contents without extracting
unzip file.zip -d out_folder/
```

## FASTA

```bash
# Count sequences
grep -c "^>" seqs.fasta

# List sequence IDs (without the ">")
grep "^>" seqs.fasta | sed 's/^>//'

# IDs only (first word of the header)
grep "^>" seqs.fasta | cut -d' ' -f1 | sed 's/^>//'

# Length of each sequence (ID <tab> length)
awk '/^>/ {if (id) print id"\t"len; id=substr($1,2); len=0; next}
     {len += length($0)}
     END {print id"\t"len}' seqs.fasta

# Total number of bases
grep -v "^>" seqs.fasta | tr -d '\n' | wc -c

# Linearize: put each sequence on a single line (makes many tasks easier)
awk '/^>/ {printf("%s%s\n", (n++ ? "\n" : ""), $0); next}
     {printf("%s", $0)}
     END {printf("\n")}' seqs.fasta > seqs.linear.fasta

# Extract sequences whose ID is in a list (ids.txt: one ID per line)
awk 'NR==FNR {ids[$1]; next}
     /^>/ {keep = (substr($1,2) in ids)}
     keep' ids.txt seqs.fasta > subset.fasta

# Remove sequences shorter than 500 bp (works on a linearized FASTA)
awk '/^>/ {h=$0; next} length($0) >= 500 {print h"\n"$0}' \
    seqs.linear.fasta > seqs.min500.fasta

# Split a multi-FASTA into one file per sequence
awk '/^>/ {if (f) close(f); f = substr($1,2) ".fasta"} {print > f}' seqs.fasta

# Shorten headers to the first word
sed '/^>/ s/ .*//' seqs.fasta > seqs.short_headers.fasta

# Add a prefix to every header
sed 's/^>/>sampleA_/' seqs.fasta

# GC content of a whole file
awk '!/^>/ {seq = seq toupper($0)}
     END {total = length(seq); gc = gsub(/[GC]/, "", seq);
          printf("GC = %.2f%%\n", 100 * gc / total)}' seqs.fasta

# Reverse complement of a single sequence
echo "ATGCGTTA" | rev | tr ACGTacgt TGCAtgca

# Concatenate many FASTA files into one
cat genomes/*.fna > all_genomes.fna
```

## FASTQ

A FASTQ record is always **4 lines**: header (`@`), sequence, `+`, qualities.

```bash
# Number of reads
echo $(( $(zcat reads.fastq.gz | wc -l) / 4 ))

# First 5 reads
zcat reads.fastq.gz | head -n 20

# FASTQ -> FASTA
zcat reads.fastq.gz | sed -n '1~4s/^@/>/p; 2~4p' > reads.fasta

# Read length distribution (length <tab> count)
zcat reads.fastq.gz | awk 'NR % 4 == 2 {print length($0)}' \
    | sort -n | uniq -c | awk '{print $2"\t"$1}'

# Mean read length
zcat reads.fastq.gz | awk 'NR % 4 == 2 {s += length($0); n++} END {print s/n}'

# Subsample the first 100,000 reads
zcat reads.fastq.gz | head -n 400000 | gzip > sub.fastq.gz

# Check that R1 and R2 have the same number of reads
for f in *_R1*.fastq.gz; do
    r2=${f/_R1/_R2}
    echo -e "$f\t$(( $(zcat "$f" | wc -l) / 4 ))\t$(( $(zcat "$r2" | wc -l) / 4 ))"
done
```

## grep: searching

```bash
grep "pattern" file               # lines containing pattern
grep -i "pattern" file            # case-insensitive
grep -v "pattern" file            # lines NOT containing pattern
grep -c "pattern" file            # count matching lines
grep -n "pattern" file            # show line numbers
grep -w "gene1" file              # whole word only (won't match gene10)
grep -F "a.b*c" file              # literal string, no regex
grep -f ids.txt file              # any pattern listed in ids.txt
grep -wFf ids.txt file            # ... exact words, fast (good for ID lists)
grep -r "pattern" folder/         # search recursively in all files
grep -l "pattern" *.tsv           # only print file names that match
grep -A 2 -B 1 "pattern" file     # 2 lines after and 1 line before each match

# Extract only the matching text (-o) with an extended regex (-E)
grep -oE 'SAM(N|EA|D)[0-9]+' table.tsv            # BioSample accessions
grep -oE 'GC[AF]_[0-9]{9}\.[0-9]+' table.tsv     # Assembly accessions
grep -oE '[SE]RR[0-9]+' table.tsv                 # SRA run accessions

# Extract and deduplicate, keeping the original order
grep -oE 'SAM(N|EA|D)[0-9]+' table.tsv | awk '!seen[$0]++' > biosamples.txt
```

## cut, sort, uniq: tables

```bash
cut -f 2 file.tsv                 # column 2 (tab-separated by default)
cut -f 1,3,5 file.tsv             # several columns
cut -f 3- file.tsv                # column 3 to the end
cut -d ',' -f 2 file.csv          # comma-separated

sort file.txt                     # alphabetical
sort -n file.txt                  # numeric
sort -k2,2nr file.tsv             # by column 2, numeric, descending
sort -t $'\t' -k3,3 -k1,1 file    # by column 3, then column 1
sort -u file.txt                  # sort and remove duplicates
sort -V files.txt                 # natural order (chr2 before chr10)

uniq -c                           # count consecutive duplicates (sort first!)
sort file.txt | uniq -c | sort -nr          # frequency table, most common first
sort file.txt | uniq -d                     # only values that are duplicated

# Frequency of values in column 4, without the header
tail -n +2 file.tsv | cut -f 4 | sort | uniq -c | sort -nr

paste file1.txt file2.txt         # put files side by side (column-wise)
paste -sd, ids.txt                # join all lines into one: id1,id2,id3
tr '\t' ','  < file.tsv > file.csv          # TSV -> CSV (only if no commas in fields)
tr -d '\r' < windows.txt > unix.txt         # remove Windows line endings
```

## awk: column processing

`awk` reads a file line by line, splits each line into columns (`$1`, `$2`, …;
`$0` is the whole line, `NF` the number of columns, `NR` the line number) and
applies `condition { action }` rules.

```bash
awk -F'\t' '{print $2}' file.tsv                 # column 2
awk -F'\t' '{print $NF}' file.tsv                # last column
awk -F'\t' '{print $(NF-1)}' file.tsv            # second-to-last column
awk -F'\t' 'NR > 1' file.tsv                     # skip header
awk -F'\t' -v OFS='\t' '{print $3, $1}' file.tsv # reorder columns, keep tabs

# Filter rows
awk -F'\t' '$5 > 1000' file.tsv                  # numeric condition
awk -F'\t' '$3 == "chromosome"' file.tsv         # exact match
awk -F'\t' '$4 ~ /Escherichia/' file.tsv         # regex match in a column
awk -F'\t' 'NR == 1 || $7 < 1e-5' blast.tsv      # keep header + filtered rows
awk -F'\t' '$NF != ""' file.tsv                  # last column not empty

# Sum, mean, min, max of a column
awk -F'\t' '{s += $2} END {print s}' file.tsv
awk -F'\t' '{s += $2; n++} END {print s/n}' file.tsv
awk -F'\t' 'NR == 1 {min = max = $2}
            {if ($2 < min) min = $2; if ($2 > max) max = $2}
            END {print min, max}' file.tsv

# Remove duplicate lines, keeping order (first occurrence)
awk '!seen[$0]++' file.txt
# ... duplicates based on one column only
awk -F'\t' '!seen[$1]++' file.tsv

# Count / sum per group (group by column 1)
awk -F'\t' '{count[$1]++} END {for (k in count) print k"\t"count[k]}' file.tsv
awk -F'\t' '{sum[$1] += $3} END {for (k in sum) print k"\t"sum[k]}' file.tsv

# Select a column by its header name
awk -F'\t' -v col="geo_loc_name" '
    NR == 1 {for (i = 1; i <= NF; i++) if ($i == col) c = i; next}
    {print $c}' file.tsv

# Add a column
awk -F'\t' -v OFS='\t' '{print $0, "sampleA"}' file.tsv
awk -F'\t' -v OFS='\t' 'NR == 1 {print $0, "len_kb"; next}
                        {print $0, $3/1000}' file.tsv

# Convert a GFF to BED (0-based start) for CDS features
awk -F'\t' -v OFS='\t' '!/^#/ && $3 == "CDS" {print $1, $4-1, $5, $9, ".", $7}' \
    annotation.gff > cds.bed
```

## sed: find and replace

```bash
sed 's/old/new/' file             # replace first match on each line
sed 's/old/new/g' file            # replace all matches
sed -i 's/old/new/g' file         # edit the file in place (careful!)
sed -i.bak 's/old/new/g' file     # in place, keeping a backup file.bak
sed -n '10,20p' file              # print lines 10 to 20
sed '1d' file                     # delete the first line (header)
sed '/^#/d' file                  # delete comment lines
sed '/^$/d' file                  # delete empty lines
sed 's/\t/,/g' file.tsv           # tabs -> commas
sed 's/^[ \t]*//; s/[ \t]*$//'    # trim leading/trailing whitespace
sed 's/.*\(GC[AF]_[0-9.]*\).*/\1/' file   # keep only the captured group
sed -E 's/(GC[AF]_[0-9]+\.[0-9]+)_.*/\1/' # same idea with extended regex
```

## Joining and comparing files

```bash
# Add info from table2 to table1 using a shared ID in column 1
# (like a SQL LEFT JOIN; missing IDs get "NA")
awk -F'\t' -v OFS='\t' 'NR==FNR {info[$1] = $2; next}
                        {print $0, ($1 in info ? info[$1] : "NA")}' \
    table2.tsv table1.tsv > joined.tsv

# Same with join (both files must be sorted on the key)
join -t $'\t' <(sort -k1,1 a.tsv) <(sort -k1,1 b.tsv) > joined.tsv

# Set operations on two lists (comm needs sorted input)
comm -12 <(sort a.txt) <(sort b.txt)     # in both
comm -23 <(sort a.txt) <(sort b.txt)     # only in a
comm -13 <(sort a.txt) <(sort b.txt)     # only in b

diff file1.txt file2.txt                 # line-by-line differences
md5sum *.fastq.gz > checksums.md5        # checksums
md5sum -c checksums.md5                  # verify downloads
```

## Loops and batch processing

```bash
# Loop over files, deriving a sample name from each
for f in reads/*_R1.fastq.gz; do
    sample=$(basename "$f" _R1.fastq.gz)
    echo "Processing $sample"
    fastp -i "$f" -I "reads/${sample}_R2.fastq.gz" \
          -o "trimmed/${sample}_R1.fastq.gz" -O "trimmed/${sample}_R2.fastq.gz"
done

# Loop over the lines of a file
while read -r acc; do
    echo "Downloading $acc"
done < accessions.txt

# Loop over a two-column TSV (sample <tab> path)
while IFS=$'\t' read -r sample path; do
    echo "$sample -> $path"
done < samples.tsv

# Run in parallel: 8 jobs at a time
ls *.fasta | xargs -P 8 -I {} prodigal -i {} -a {}.faa -q
parallel -j 8 'gzip {}' ::: *.fastq                       # GNU parallel

# Useful string manipulations inside loops
f="sample1_R1.fastq.gz"
echo "${f%.fastq.gz}"       # remove suffix   -> sample1_R1
echo "${f%%_*}"             # up to first _   -> sample1
echo "${f/_R1/_R2}"         # replace         -> sample1_R2.fastq.gz
echo "$(basename /a/b/c.fa .fa)"   # strip path and extension -> c

# Stop a script at the first error, and on unset variables
set -euo pipefail
```

## Downloading data from NCBI

```bash
# Direct download
wget https://example.org/file.fa.gz
curl -L -O https://example.org/file.fa.gz
wget -i urls.txt                          # download every URL in a file

# NCBI Datasets CLI: genomes by accession
datasets download genome accession GCF_000005845.2 \
    --include genome,protein,gff3 --filename ecoli.zip
datasets download genome accession --inputfile assemblies.txt \
    --include genome --filename genomes.zip
# Genome metadata as a table
datasets summary genome taxon "Campylobacter jejuni" \
    --assembly-level complete --as-json-lines \
  | dataformat tsv genome \
    --fields accession,organism-name,assmstats-total-sequence-len,assminfo-biosample-accession

# Entrez Direct (EDirect)
efetch -db nucleotide -id NC_000913.3 -format fasta > ecoli.fasta
efetch -db nucleotide -id NC_000913.3 -format gb > ecoli.gbk
esearch -db assembly -query "Campylobacter jejuni[Organism] AND complete genome[filter]" \
  | esummary | xtract -pattern DocumentSummary -element AssemblyAccession BioSampleAccn

# SRA reads (sra-tools)
prefetch SRR1234567
fasterq-dump --split-files --threads 8 SRR1234567
```

## Common bioinformatics tools

```bash
# samtools
samtools faidx genome.fa                       # index a FASTA
samtools faidx genome.fa chr1:1000-2000        # extract a region
cut -f1,2 genome.fa.fai                        # sequence names and lengths
samtools view -c aln.bam                       # count alignments
samtools view -c -F 4 aln.bam                  # count mapped reads
samtools flagstat aln.bam                      # mapping summary
samtools sort -@ 8 -o aln.sorted.bam aln.bam
samtools index aln.sorted.bam
samtools depth -a aln.sorted.bam | awk '{s += $3} END {print s/NR}'  # mean depth

# seqkit (fast FASTA/FASTQ swiss-army knife)
seqkit stats *.fasta                           # counts, lengths, N50 (-a)
seqkit seq -m 500 seqs.fasta                   # keep sequences >= 500 bp
seqkit grep -f ids.txt seqs.fasta              # extract by ID list
seqkit fx2tab -n -l -g seqs.fasta              # name, length, GC per sequence
seqkit rmdup -s seqs.fasta                     # remove duplicate sequences

# bedtools
bedtools intersect -a genes.bed -b peaks.bed -u      # genes overlapping peaks
bedtools getfasta -fi genome.fa -bed regions.bed -fo regions.fa
```

## HPC and long-running jobs

```bash
nohup ./long_job.sh > job.log 2>&1 &       # keep running after logout
tmux new -s analysis                       # persistent session (Ctrl-b d to detach)
tmux attach -t analysis
htop                                       # monitor CPU/memory
nproc                                      # number of CPU cores
free -h                                    # memory available

# SLURM
sbatch job.sh                              # submit
squeue -u $USER                            # my jobs
scancel <jobid>                            # cancel
sacct -j <jobid> --format=JobID,State,Elapsed,MaxRSS   # usage after finishing
```

Minimal SLURM script:

```bash
#!/bin/bash
#SBATCH --job-name=assembly
#SBATCH --cpus-per-task=16
#SBATCH --mem=32G
#SBATCH --time=24:00:00
#SBATCH --output=logs/%x_%j.out

set -euo pipefail
spades.py -1 R1.fastq.gz -2 R2.fastq.gz -o spades_out -t "$SLURM_CPUS_PER_TASK"
```

---

# Biopython

Install with `pip install biopython` or `conda install -c conda-forge biopython`.
Examples target Biopython ≥ 1.80.

## Reading and writing sequences

```python
from Bio import SeqIO

# Iterate over a FASTA file
for record in SeqIO.parse("seqs.fasta", "fasta"):
    print(record.id, len(record.seq), record.description)

# Read a file that contains exactly one sequence
record = SeqIO.read("single.fasta", "fasta")

# Load everything into a dictionary {id: record} (small files)
records = SeqIO.to_dict(SeqIO.parse("seqs.fasta", "fasta"))
print(records["seq1"].seq)

# Index a large file without loading it into memory
index = SeqIO.index("big.fasta", "fasta")
print(index["seq42"].seq)

# Filter by length and write the result
long_seqs = (r for r in SeqIO.parse("seqs.fasta", "fasta") if len(r) >= 500)
count = SeqIO.write(long_seqs, "seqs.min500.fasta", "fasta")
print(f"{count} sequences written")

# Extract sequences whose ID is in a list
with open("ids.txt") as fh:
    wanted = {line.strip() for line in fh if line.strip()}
subset = (r for r in SeqIO.parse("seqs.fasta", "fasta") if r.id in wanted)
SeqIO.write(subset, "subset.fasta", "fasta")

# Convert between formats
SeqIO.convert("genome.gbk", "genbank", "genome.fasta", "fasta")
SeqIO.convert("reads.fastq", "fastq", "reads.fasta", "fasta")

# Read gzip-compressed files
import gzip
with gzip.open("seqs.fasta.gz", "rt") as fh:
    for record in SeqIO.parse(fh, "fasta"):
        print(record.id)

# Length table (ID <tab> length)
with open("lengths.tsv", "w") as out:
    for r in SeqIO.parse("seqs.fasta", "fasta"):
        out.write(f"{r.id}\t{len(r)}\n")

# Rename sequences
def renamed(records, prefix):
    for i, r in enumerate(records, 1):
        r.id = f"{prefix}_{i}"
        r.description = ""
        yield r

SeqIO.write(renamed(SeqIO.parse("seqs.fasta", "fasta"), "contig"),
            "renamed.fasta", "fasta")
```

## Working with sequences

```python
from Bio.Seq import Seq
from Bio.SeqRecord import SeqRecord
from Bio.SeqUtils import gc_fraction

dna = Seq("ATGGCCATTGTAATGGGCCGCTGAAAGGGTGCCCGATAG")

dna.complement()
dna.reverse_complement()
dna.transcribe()                       # DNA -> RNA
dna.translate()                        # standard code, '*' for stops
dna.translate(table=11, to_stop=True)  # bacterial code, stop at first stop
dna[0:9]                               # slicing works like strings
dna.count("G")
gc_fraction(dna)                       # 0.0-1.0

# Translate in all 6 reading frames
for strand, seq in [(+1, dna), (-1, dna.reverse_complement())]:
    for frame in range(3):
        sub = seq[frame:]
        sub = sub[: len(sub) - len(sub) % 3]       # whole codons only
        print(strand, frame, sub.translate(table=11))

# Build a record and write it
rec = SeqRecord(dna, id="my_gene", description="example sequence")
SeqIO.write([rec], "my_gene.fasta", "fasta")

# Translate a nucleotide FASTA of CDSs into proteins
proteins = (
    SeqRecord(r.seq.translate(table=11, to_stop=True), id=r.id, description="")
    for r in SeqIO.parse("cds.fna", "fasta")
)
SeqIO.write(proteins, "proteins.faa", "fasta")
```

## GenBank files and features

```python
from Bio import SeqIO

for record in SeqIO.parse("genome.gbk", "genbank"):
    print(record.id, record.description, len(record))
    print(record.annotations.get("organism"))

    for feature in record.features:
        if feature.type != "CDS":
            continue
        q = feature.qualifiers
        locus = q.get("locus_tag", ["NA"])[0]
        product = q.get("product", ["NA"])[0]
        start = int(feature.location.start) + 1   # Biopython is 0-based
        end = int(feature.location.end)
        strand = "+" if feature.location.strand == 1 else "-"
        print(locus, start, end, strand, product)

        nucleotide = feature.extract(record.seq)  # handles strand and joins
        protein = q.get("translation", [""])[0]

# Write all CDS proteins to a FASTA
from Bio.SeqRecord import SeqRecord
from Bio.Seq import Seq

def cds_proteins(path):
    for record in SeqIO.parse(path, "genbank"):
        for f in record.features:
            if f.type == "CDS" and "translation" in f.qualifiers:
                yield SeqRecord(
                    Seq(f.qualifiers["translation"][0]),
                    id=f.qualifiers.get("locus_tag", ["NA"])[0],
                    description=f.qualifiers.get("product", [""])[0],
                )

SeqIO.write(cds_proteins("genome.gbk"), "proteins.faa", "fasta")

# Find features overlapping a position
pos = 150000
hits = [f for f in record.features if pos in f.location and f.type == "CDS"]
```

## FASTQ and quality scores

```python
import gzip
from statistics import mean
from Bio import SeqIO

with gzip.open("reads.fastq.gz", "rt") as fh:
    for record in SeqIO.parse(fh, "fastq"):
        quals = record.letter_annotations["phred_quality"]  # list of ints
        print(record.id, len(record), mean(quals))
        break

# Keep reads with mean quality >= 20 and length >= 50
def good_reads(handle, min_q=20, min_len=50):
    for r in SeqIO.parse(handle, "fastq"):
        if len(r) >= min_len and mean(r.letter_annotations["phred_quality"]) >= min_q:
            yield r

with gzip.open("reads.fastq.gz", "rt") as fin, gzip.open("filtered.fastq.gz", "wt") as fout:
    n = SeqIO.write(good_reads(fin), fout, "fastq")
print(f"{n} reads kept")

# Fast iteration for very large files (tuples of strings, no SeqRecord overhead)
from Bio.SeqIO.QualityIO import FastqGeneralIterator
with gzip.open("reads.fastq.gz", "rt") as fh:
    n_reads = sum(1 for _ in FastqGeneralIterator(fh))
```

## NCBI Entrez

NCBI asks you to identify yourself. An API key (free, from your NCBI account)
raises the limit from 3 to 10 requests per second.

```python
from Bio import Entrez, SeqIO

Entrez.email = "you@example.com"     # required
# Entrez.api_key = "YOUR_API_KEY"    # optional

# Search: get IDs matching a query
handle = Entrez.esearch(db="nucleotide",
                        term="Campylobacter jejuni[Organism] AND complete genome[Title]",
                        retmax=20)
result = Entrez.read(handle)
handle.close()
print(result["Count"], result["IdList"])

# Fetch sequences as FASTA or GenBank
handle = Entrez.efetch(db="nucleotide", id="NC_000913.3", rettype="fasta", retmode="text")
record = SeqIO.read(handle, "fasta")
handle.close()

handle = Entrez.efetch(db="nucleotide", id="NC_000913.3", rettype="gbwithparts", retmode="text")
SeqIO.write(SeqIO.read(handle, "genbank"), "ecoli.gbk", "genbank")
handle.close()

# Fetch many IDs at once (batches of ~200)
ids = ["NC_000913.3", "NC_002163.1"]
handle = Entrez.efetch(db="nucleotide", id=",".join(ids), rettype="fasta", retmode="text")
records = list(SeqIO.parse(handle, "fasta"))
handle.close()

# Summaries (lightweight metadata) for the IDs found by esearch
handle = Entrez.esummary(db="nucleotide", id=",".join(result["IdList"]))
summaries = Entrez.read(handle)
handle.close()
for s in summaries:
    print(s["AccessionVersion"], s["Title"], int(s["Length"]))

# Links between databases, e.g. nucleotide -> biosample
handle = Entrez.elink(dbfrom="nucleotide", db="biosample", id=result["IdList"][0])
links = Entrez.read(handle)
handle.close()
biosample_uids = [l["Id"] for db in links[0]["LinkSetDb"] for l in db["Link"]]

# BioSample attributes (geographic location, host, isolation source...)
# Entrez.read() does not parse BioSample XML well, so use ElementTree
import xml.etree.ElementTree as ET

handle = Entrez.efetch(db="biosample", id="SAMN08180388", retmode="xml")
root = ET.fromstring(handle.read())
handle.close()
for sample in root.iter("BioSample"):
    attrs = {a.get("harmonized_name") or a.get("attribute_name"): a.text
             for a in sample.iter("Attribute")}
    print(sample.get("accession"), attrs.get("geo_loc_name"), attrs.get("host"))
```

## Pairwise alignment

```python
from Bio import Align
from Bio.Align import substitution_matrices

# Global DNA alignment
aligner = Align.PairwiseAligner()
aligner.mode = "global"            # or "local"
aligner.match_score = 2
aligner.mismatch_score = -1
aligner.open_gap_score = -5
aligner.extend_gap_score = -1

alignments = aligner.align("GATTACAGATTACA", "GATCACAGTTACA")
best = alignments[0]
print(best.score)
print(best)

# Score only (faster when you don't need the alignment)
aligner.score("GATTACA", "GATCACA")

# Protein local alignment with BLOSUM62
aligner = Align.PairwiseAligner()
aligner.mode = "local"
aligner.substitution_matrix = substitution_matrices.load("BLOSUM62")
aligner.open_gap_score = -11
aligner.extend_gap_score = -1
best = aligner.align("MKTAYIAKQRQISFVKSHFSRQ", "MKTAYIAKQRQLSFVKSHF")[0]
print(best)

# Percent identity over aligned columns
counts = best.counts()
print(100 * counts.identities / (counts.identities + counts.mismatches))
```

## Multiple sequence alignments

```python
from Bio import AlignIO
from collections import Counter

aln = AlignIO.read("alignment.fasta", "fasta")
print(f"{len(aln)} sequences, {aln.get_alignment_length()} columns")

for record in aln:
    print(record.id, record.seq[:50])

aln[:, 100:200]                       # slice columns (a sub-alignment)
column = aln[:, 10]                   # a single column as a string

# Convert formats (e.g. for RAxML / PhyML)
AlignIO.convert("alignment.fasta", "fasta", "alignment.phy", "phylip-relaxed")

# Simple majority consensus
consensus = "".join(
    Counter(aln[:, i]).most_common(1)[0][0]
    for i in range(aln.get_alignment_length())
)

# Fraction of gaps per sequence
for record in aln:
    print(record.id, record.seq.count("-") / len(record.seq))
```

## Phylogenetic trees

```python
from Bio import Phylo

tree = Phylo.read("tree.nwk", "newick")
Phylo.draw_ascii(tree)                     # quick look in the terminal

leaves = [t.name for t in tree.get_terminals()]
print(len(leaves), leaves[:5])

# Root with an outgroup and write the tree back out
tree.root_with_outgroup("Outgroup_species")
Phylo.write(tree, "tree.rooted.nwk", "newick")

# Distance between two leaves
tree.distance("taxonA", "taxonB")

# Most recent common ancestor of a group and its leaves
mrca = tree.common_ancestor("taxonA", "taxonB")
print([t.name for t in mrca.get_terminals()])

# Prune a leaf
tree.prune("taxonC")

# Plot with matplotlib
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(8, 10))
Phylo.draw(tree, axes=ax, do_show=False)
fig.savefig("tree.pdf")
```

## Parsing BLAST results

Run BLAST with tabular output: `blastp -query q.faa -db db -outfmt 6 -out hits.tsv`.

```python
from Bio import SearchIO

# Best hit per query from tabular (outfmt 6) output
for qresult in SearchIO.parse("hits.tsv", "blast-tab"):
    best_hit = qresult.hits[0]
    best_hsp = best_hit.hsps[0]
    print(qresult.id, best_hit.id, best_hsp.ident_pct, best_hsp.evalue, best_hsp.bitscore)

# Keep hits with e-value < 1e-10 and identity >= 40%
for qresult in SearchIO.parse("hits.tsv", "blast-tab"):
    good = qresult.hsp_filter(lambda h: h.evalue < 1e-10 and h.ident_pct >= 40)
    for hit in good:
        print(qresult.id, hit.id)

# Index a large BLAST XML (outfmt 5) and access a query by ID
idx = SearchIO.index("hits.xml", "blast-xml")
print(idx["query_1"])
```

Tabular BLAST output is also easy to handle with plain Unix tools:

```bash
# Column names for -outfmt 6:
# qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore

awk -F'\t' '!seen[$1]++' hits.tsv                       # best hit per query (BLAST order)
sort -k1,1 -k12,12gr hits.tsv | awk '!seen[$1]++'       # ... by highest bitscore
awk -F'\t' '$3 >= 90 && $11 < 1e-20' hits.tsv           # filter by identity and e-value
cut -f1 hits.tsv | sort -u | wc -l                      # queries with at least one hit
```

---

# Regex quick reference

| Pattern | Matches |
|---|---|
| `.` | any single character |
| `^` / `$` | start / end of line |
| `[ACGT]` | one of these characters |
| `[^ACGT]` | any character except these |
| `[0-9]`, `[A-Z]` | a digit, an uppercase letter |
| `*` | 0 or more of the previous item |
| `+` | 1 or more (extended regex: `grep -E`, `sed -E`) |
| `?` | 0 or 1 (extended regex) |
| `{n}`, `{n,m}` | exactly n, between n and m (extended regex) |
| `(a\|b)` | a or b (extended regex) |
| `\t` | tab (awk, sed, `grep -P`) |
| `\b` | word boundary (`grep -P`) |

Common accession patterns:

| Type | Example | Regex (`grep -oE`) |
|---|---|---|
| BioSample | `SAMN02604091`, `SAMEA1705929`, `SAMD00620689` | `SAM(N\|EA\|D)[0-9]+` |
| BioProject | `PRJNA224116` | `PRJ(NA\|EB\|DB)[0-9]+` |
| Assembly | `GCF_000005845.2` | `GC[AF]_[0-9]{9}\.[0-9]+` |
| SRA run | `SRR1234567`, `ERR123456` | `[SED]RR[0-9]+` |
| RefSeq nucleotide | `NC_000913.3`, `NZ_CP012345.1` | `N[CZ]_[A-Z0-9]+\.[0-9]+` |
| RefSeq protein | `WP_000123456.1` | `[WNXY]P_[0-9]+\.[0-9]+` |
