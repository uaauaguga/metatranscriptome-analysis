# Bacteria noncoding transcripts analysis

- This pipeline takes paired metagenomic sequencing (MGX) and metatranscriptomic sequencing (MTX) data as input, and annotates intergenic regions with RNA expression
- Supports paired end / single end data

## Preprocess MGX reads

- Trim adaptor, run fastqc
- Remove unwanted sequence (optional)
- Run metaphlan for taxonomy profiling

```bash
# paired end data
snakemake --snakefile snakefiles/preprocessing.snakefile --configfile config/preprocessing/test-pe.mgx.yaml

# single end data
snakemake --snakefile snakefiles/preprocessing.snakefile --configfile config/preprocessing/test-se.mgx.yaml
```

## Preprocess MTX reads

- Trim adaptor, run fastqc
- Remove unwanted sequence (optional)
- Run metaphlan for taxonomy profiling
- Infer strandness of the RNA library based on marker gene mapping result

```bash
# paired end data
snakemake --snakefile snakefiles/preprocessing.snakefile --configfile config/preprocessing/test-pe.mtx.yaml

# single end data
snakemake --snakefile snakefiles/preprocessing.snakefile --configfile config/preprocessing/test-se.mtx.yaml
```

## Assemble MGX reads and annotate contigs

- Assemble MGX reads with megahit
- Run prodigal for gene prediction
- Annotate predicted gene with Pfam & hmmsearch
- Search contig for known noncoding RNA with Rfam & cmsearch (optional)

```bash
# paired end data
snakemake --snakefile snakefiles/mgx-analysis.snakefile --configfile config/mgx-analysis/test-pe.yaml

# single end data
snakemake --snakefile snakefiles/mgx-analysis.snakefile --configfile config/mgx-analysis/test-se.yaml
```

## Mapping MTX reads

- Map MTX reads to paired contigs
- Assemble transcripts with stringtie
- Annotate transcripts in a gene centric manner

```bash
# paired end data
snakemake --snakefile snakefiles/mtx-analysis.with.mgx.snakefile --configfile config/mtx-analysis-with-mgx/test-pe.yaml

# single end data
snakemake --snakefile snakefiles/mtx-analysis.with.mgx.snakefile --configfile config/mtx-analysis-with-mgx/test-se.yaml
```




