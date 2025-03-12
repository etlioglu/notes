# Genomes

It is probably better to use a dedicated tool like [refgenie](http://refgenie.databio.org/en/latest/) or the official
[ENSEMBL REST API](https://rest.ensembl.org/) but this document goes over downloading genomes and annotations from
[ENSEMBL's FTP server](https://ftp.ensembl.org/) manually. Adapted from
[here](https://nf-co.re/docs/usage/reference_genomes).

## Genome

    wget https://ftp.ensembl.org/pub/release-113/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
    wget -O genome_checksums.txt https://ftp.ensembl.org/pub/release-113/fasta/homo_sapiens/dna/CHECKSUMS

Compare checksums, ENSEMBL uses `sum`:

    sum Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
    grep 'Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz' genome_checksums.txt | cut -d " " -f1,2

## Annotation

    wget https://ftp.ensembl.org/pub/release-113/gtf/homo_sapiens/Homo_sapiens.GRCh38.113.gtf.gz
    wget -O gtf_checksums.txt https://ftp.ensembl.org/pub/release-113/gtf/homo_sapiens/CHECKSUMS

Compare checksums:

    sum Homo_sapiens.GRCh38.113.gtf.gz
    grep 'Homo_sapiens.GRCh38.113.gtf.gz' gtf_checksums.txt | cut -d " " -f1,2

## nfch

Add the full paths of the downloaded and integrity checked genome and annotation files to the `genomes.json` file at
the top level genomes directory.
