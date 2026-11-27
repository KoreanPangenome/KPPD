# A Draft Korean Pangenome Reference: KPPD

**Last updated:** 2026-05-15
**Status:** Draft Release  


## Update Log
| Date | Version | Update |
|------|---------|--------|
| 2026-05-15 | Draft v1.0.1 | Added srWGS mapping and graph-based variant calling workflow using `vg haplotypes`, `vg giraffe`, `vg pack`, and `vg call`. |
| 2025-12-09 | Draft v1.0.0 | Initial draft release of the KPPD pangenome graph, haplotype panel, VCF files, and checksum file. |



---

## Table of Contents

1. [Overview](#1-overview)  
2. [Analysis Workflow](#2-analysis-workflow)  
3. [Data Downloads](#3-data-downloads)  
4. [Mapping srWGS to the Pangenome Graph and Variant Calling](#4-mapping-srwgs-to-the-pangenome-graph-and-variant-calling)  
5. [Citation](#5-citation)  
6. [Contact](#6-contact)  

---

## 1. Overview

**A Draft Korean Pangenome Reference (KPPD)** is a population-scale Korean pangenome reference constructed from **132 deep-sequenced Korean individuals**.

The dataset integrates telomere-to-telomere assemblies and high-quality long-read assemblies to enable accurate structural variant discovery, genome graph construction, and haplotype resolution.

### Composition of the Dataset

| Category | Individuals | Sequencing | Notes |
|----------|-------------|------------|-------|
| **T2T-level assemblies** | 4 | PacBio Revio 60×, ONT Ultra-Long 60×, Omni-C | Full telomere-to-telomere resolution |
| **Non-T2T long-read assemblies** | 128 | PacBio Revio ~30× | High-contiguity diploid assemblies |

**Total:** 132 Korean genomes were used to construct the pangenome graph and variant catalogue.

---

## 2. Analysis Workflow

The Korean Pangenome Draft (KPPD) was constructed through a multi-stage workflow integrating long-read assemblies, graph construction, and haplotype-aware read alignment.

---

### 2.1 Sequencing Data Generation

A total of **132 genomes** were sequenced:

- **128 PacBio Revio HiFi datasets**
  - ~30× depth
  - N50 ~16 kb
  - Q28 median

- **4 T2T-level datasets**
  - PacBio Revio HiFi ~60×
  - ONT Ultra-Long ~60×
  - ONT Ultra-Long N50 ~90 kb
  - Dovetail Omni-C

These datasets were used to generate high-quality haplotype-resolved assemblies.

---

### 2.2 Assembly Construction

Assemblies were constructed using:

**Hifiasm v0.19.9-r616**

For **128 non-T2T samples**:

- Hifiasm produced partially phased contigs per sample
- Hap1 and Hap2 assemblies were generated
- Total: 256 raw assemblies

For **4 T2T-level samples**:

- Hifiasm generated fully phased T2T-level haplotype assemblies
- Total: 8 raw assemblies

Resulting assemblies included both partially phased and fully phased haplotype contigs depending on sequencing depth and data type.

---

### 2.3 Assembly Correction

Raw assemblies were polished and corrected using self-alignment of PacBio HiFi reads.

Tool used:

- **Inspector v1.3.1**

Final output:

- **264 corrected haplotype assemblies**

Assembly summary:

| Assembly type | Number of haplotypes | Mean contigs | Mean QV |
|---------------|----------------------|--------------|---------|
| HiFi-only haplotypes | 256 | ~561 | ~53 |
| T2T-level haplotypes | 8 | ~102 | ~54 |

Corrected haplotypes were used as input for graph construction.

---

### 2.4 Draft Korean Pangenome Graph Construction

The **Draft Korean Pangenome Graph** was built using:

- **Minigraph-cactus v2.9.3**

Input references and assemblies:

- CHM13 v2.0
- GRCh38
- 132 Korean haplotype-resolved assemblies

Graph output summary:

| Metric | Value |
|--------|-------|
| Nodes | 123 M |
| Edges | 171 M |
| Graph size | 3.45 GB |
| Graph formats | GBZ, GFA |

This graph represents Korean haplotype diversity integrated on the CHM13 backbone.

---

### 2.5 Haplotype-Aware Short-Read Alignment

Short reads were aligned to the pangenome graph using:

- **vg giraffe v1.6.7**

Alignment output:

- GAM format

A haplotype depth filter was applied using:

- **vg clip v1.6.7**

Filtering thresholds:

| Haplotype source | Depth threshold | Allele frequency threshold |
|------------------|----------------|----------------------------|
| HPRC haplotypes | >9× | AF > 0.1 |
| Korean pangenome haplotypes | >2× | AF > 0.01 |
| Korean haplotypes | >53× | AF > 0.2 |

These filters refine haplotype representation for variant interpretation.

---

## 3. Data Downloads

The following dataset files are available via Google Drive.

| Filename | Description | Link |
|----------|-------------|------|
| **kor132.chm13v2.gfa.gz** | Multi-assembly pangenome graph in GFA format | [Download](https://drive.google.com/file/d/1aG5d70RsDNPzGBim7Tax-cDtG1dmAQdY/view?usp=drive_link) |
| **kor132.chm13v2.gbz** | GBZ-format graph compatible with vg | [Download](https://drive.google.com/file/d/1y84nTxuCevpvNlsO8KyDGiV7RyzI2O59/view?usp=drive_link) |
| **kor132.chm13v2.hapl** | Population haplotype panel | [Download](https://drive.google.com/file/d/1cwrrG7F0Xupi2S2UpN8KMNFDSzYPrH5z/view?usp=drive_link) |
| **kor132.chm13v2.sv.gfa.fa.gz** | SV graph sequence file | [Download](https://drive.google.com/file/d/1OLH_PjftZO6KIXXAC4aqtc49Quk3agX5/view?usp=drive_link) |
| **kor132.chm13v2.wave.vcf.gz** | Variant calls in CHM13 coordinates | [Download](https://drive.google.com/file/d/1o2kNQdoMR2y5AvXgoS3yUNmVYVNMtMEO/view?usp=drive_link) |
| **kor132.chm13v2.GRCh38.wave.vcf.gz** | Variant calls in GRCh38 coordinates | [Download](https://drive.google.com/file/d/1_FqGHXKGGB1fnmQt7sVndiSMXbHTAZz_/view?usp=drive_link) |
| **upload_md5sum.txt** | MD5 checksum file | [Download](https://drive.google.com/file/d/1KhzOZ15xamKJ9ceK356ZBKf0_kMWaZuV/view?usp=drive_link) |


### T2T-level Genome Assemblies

Haplotype-resolved T2T-level genome assemblies from four Korean individuals (eight haplotypes in total) are publicly available as part of the Korean Pangenome Project (KPP).

| Dataset | Description | Link |
|---------|-------------|------|
| **KPP T2T-level assemblies** | Haplotype-resolved genome assemblies from 4 individuals (8 haplotypes) | [Download](YOUR_GOOGLE_DRIVE_LINK) |

---

## 4. Mapping srWGS to the Pangenome Graph and Variant Calling

This section describes how to map short-read whole-genome sequencing data, referred to here as **srWGS**, to the KPPD pangenome graph and call variants from graph alignment files.

The workflow consists of three major steps:

1. Build a k-mer index from srWGS reads using **KMC**
2. Generate a sample-specific haplotype-sampled pangenome graph using **vg haplotypes**
3. Map srWGS reads to the sampled graph and call variants using **vg giraffe**, **vg pack**, and **vg call**

---

### 4.1 Software Requirements

The following software is required.

| Software | Version used | Purpose | Link |
|----------|--------------|---------|------|
| **vg** | v1.74.1 | Graph mapping, haplotype sampling, snarl detection, and variant calling | [vg GitHub](https://github.com/vgteam/vg) |
| **KMC** | v3.2.4 | k-mer counting from srWGS reads | [KMC GitHub](https://github.com/refresh-bio/KMC) |

Example installation:

```bash
# Download vg
wget https://github.com/vgteam/vg/releases/download/v1.74.1/vg
chmod +x vg

# Download KMC
wget https://github.com/refresh-bio/KMC/releases/download/v3.2.4/KMC3.2.4.linux.x64.tar.gz
tar -zxvf KMC3.2.4.linux.x64.tar.gz
```

Make sure the `vg`, `kmc`, and `kmc_tools` executables are available in your `PATH`.

---

### 4.2 Input Files

This workflow requires the following KPPD files:

| File | Description |
|------|-------------|
| `kor132.chm13v2.gbz` | KPPD pangenome graph in GBZ format |
| `kor132.chm13v2.hapl` | KPPD population haplotype panel |

Example srWGS input files:

```bash
srWGS1_R1.fastq.gz
srWGS1_R2.fastq.gz
srWGS2_R1.fastq.gz
srWGS2_R2.fastq.gz
```

Set the working directory:

```bash
WORKING_DIR=$(pwd)
```

---

### 4.3 Build k-mer Index from srWGS Reads

First, generate a k-mer index from each srWGS sample using **KMC**.

```bash
SAMPLES=(srWGS1 srWGS2)

WORKING_DIR=$(pwd)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[KMC] Processing ${SAMPLE}"

    ls | grep ${SAMPLE} | grep "fastq.gz$" | sort > ${SAMPLE}.input_fastq_files.txt

    kmc \
        -k29 \
        -m128 \
        -okff \
        -t100 \
        @${SAMPLE}.input_fastq_files.txt \
        ${SAMPLE}.srWGS \
        ${WORKING_DIR}
done
```

Main options:

| Option | Description |
|--------|-------------|
| `-k29` | k-mer length |
| `-m128` | Maximum RAM usage in GB |
| `-okff` | Output in KFF format |
| `-t100` | Number of threads |
| `@input_fastq_files.txt` | List of input FASTQ files |

This step generates KFF files:

```bash
srWGS1.srWGS.kff
srWGS2.srWGS.kff
```

---

### 4.4 Generate a Sample-Specific Haplotype-Sampled Pangenome Graph

The k-mer index is used to select haplotype paths that are most similar to each srWGS sample.

This produces a smaller sample-specific pangenome graph for read mapping and variant calling.

```bash
SAMPLES=(srWGS1 srWGS2)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[vg haplotypes] Sampling haplotypes for ${SAMPLE}"

    KFF=${SAMPLE}.srWGS.kff

    vg haplotypes \
        --verbosity 2 \
        --threads 100 \
        --include-reference \
        --diploid-sampling \
        --haplotype-input kor132.chm13v2.hapl \
        --kmer-input ${KFF} \
        --gbz-output ${SAMPLE}_sampled.pangenome.gbz \
        kor132.chm13v2.gbz

    echo "[vg snarls] Computing snarls for ${SAMPLE}"

    vg snarls \
        --threads 100 \
        ${SAMPLE}_sampled.pangenome.gbz \
        > ${SAMPLE}_sampled.pangenome.gbz.snarls
done
```

Main options:

| Option | Description |
|--------|-------------|
| `--include-reference` | Include named reference paths in the output graph |
| `--diploid-sampling` | Select the best pair of sampled haplotypes |
| `--haplotype-input` | Input haplotype panel |
| `--kmer-input` | KFF file generated from srWGS reads |
| `--gbz-output` | Output haplotype-sampled GBZ graph |

Output files:

```bash
srWGS1_sampled.pangenome.gbz
srWGS1_sampled.pangenome.gbz.snarls

srWGS2_sampled.pangenome.gbz
srWGS2_sampled.pangenome.gbz.snarls
```

---

### 4.5 Generate a Multi-Sample Haplotype-Sampled Pangenome Graph

Multiple srWGS samples can also be combined to generate a shared haplotype-sampled graph.

```bash
SAMPLE=srWGS_multi

WORKING_DIR=$(pwd)

ls | grep "srWGS[1-2]" | grep "fastq.gz$" | sort > ${SAMPLE}.input_fastq_files.txt

kmc \
    -k29 \
    -m128 \
    -okff \
    -t100 \
    @${SAMPLE}.input_fastq_files.txt \
    ${SAMPLE}.srWGS \
    ${WORKING_DIR}

KFF=${SAMPLE}.srWGS.kff

vg haplotypes \
    --verbosity 2 \
    --threads 100 \
    --include-reference \
    --diploid-sampling \
    --haplotype-input kor132.chm13v2.hapl \
    --kmer-input ${KFF} \
    --gbz-output ${SAMPLE}_sampled.pangenome.gbz \
    kor132.chm13v2.gbz

vg snarls \
    --threads 100 \
    ${SAMPLE}_sampled.pangenome.gbz \
    > ${SAMPLE}_sampled.pangenome.gbz.snarls
```

Output files:

```bash
srWGS_multi_sampled.pangenome.gbz
srWGS_multi_sampled.pangenome.gbz.snarls
```

---

### 4.6 Map srWGS Reads to the Haplotype-Sampled Pangenome Graph

Short reads are mapped to the sampled graph using **vg giraffe**.

```bash
SAMPLES=(srWGS1 srWGS2)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[vg giraffe] Mapping ${SAMPLE}"

    READ1=${SAMPLE}_R1.fastq.gz
    READ2=${SAMPLE}_R2.fastq.gz

    GBZ=${SAMPLE}_sampled.pangenome.gbz
    GAM=${SAMPLE}.srWGS.pangenome_hapl.gam

    vg giraffe \
        --progress \
        --threads 100 \
        --gbz-name ${GBZ} \
        --fastq-in ${READ1} \
        --fastq-in ${READ2} \
        > ${GAM} \
        2> ${GAM}.log

    vg stats \
        --threads 100 \
        --alignments ${GAM} \
        > ${GAM}.stats.txt
done
```

Output files:

```bash
srWGS1.srWGS.pangenome_hapl.gam
srWGS1.srWGS.pangenome_hapl.gam.log
srWGS1.srWGS.pangenome_hapl.gam.stats.txt
```

---

### 4.7 Generate Read Support with vg pack

The graph alignment file is converted into read support information using **vg pack**.

```bash
SAMPLES=(srWGS1 srWGS2)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[vg pack] Packing alignments for ${SAMPLE}"

    GBZ=${SAMPLE}_sampled.pangenome.gbz
    GAM=${SAMPLE}.srWGS.pangenome_hapl.gam
    PACK=${SAMPLE}.srWGS.pangenome_hapl.gam.pack

    vg pack \
        --threads 100 \
        --xg ${GBZ} \
        --gam ${GAM} \
        --output ${PACK} \
        --min-mapq 5
done
```

Main options:

| Option | Description |
|--------|-------------|
| `--xg` | Input graph. GBZ can be used as the graph basis |
| `--gam` | Input GAM alignment file |
| `--output` | Output pack file |
| `--min-mapq 5` | Ignore reads with mapping quality below 5 |

---

### 4.8 Call Variants from Graph Alignment

Variants can be called on either the **CHM13 v2.0** or **GRCh38** coordinate system depending on the selected reference path.

---

#### 4.8.1 Variant Calling on CHM13 Coordinates

```bash
SAMPLES=(srWGS1 srWGS2)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[vg call] Calling variants for ${SAMPLE} on CHM13 coordinates"

    GBZ=${SAMPLE}_sampled.pangenome.gbz
    SNARLS=${SAMPLE}_sampled.pangenome.gbz.snarls
    PACK=${SAMPLE}.srWGS.pangenome_hapl.gam.pack
    VCF=${SAMPLE}_sampled.pangenome.chm13v2.vcf

    vg call \
        --threads 100 \
        --ref-sample "CHM13v2" \
        ${GBZ} \
        --genotype-snarls \
        --snarls ${SNARLS} \
        --pack ${PACK} \
        --sample ${SAMPLE} \
        --gbz \
        > ${VCF}
done
```

---

#### 4.8.2 Variant Calling on GRCh38 Coordinates

```bash
SAMPLES=(srWGS1 srWGS2)

for SAMPLE in ${SAMPLES[@]}
do
    echo "[vg call] Calling variants for ${SAMPLE} on GRCh38 coordinates"

    GBZ=${SAMPLE}_sampled.pangenome.gbz
    SNARLS=${SAMPLE}_sampled.pangenome.gbz.snarls
    PACK=${SAMPLE}.srWGS.pangenome_hapl.gam.pack
    VCF=${SAMPLE}_sampled.pangenome.grch38.vcf

    vg call \
        --threads 100 \
        --ref-sample "GRCh38" \
        ${GBZ} \
        --genotype-snarls \
        --snarls ${SNARLS} \
        --pack ${PACK} \
        --sample ${SAMPLE} \
        --gbz \
        > ${VCF}
done
```

Main options:

| Option | Description |
|--------|-------------|
| `--ref-sample` | Reference path used for VCF coordinates |
| `--genotype-snarls` | Genotype all snarls, including reference calls |
| `--snarls` | Precomputed snarls from `vg snarls` |
| `--pack` | Read support file generated by `vg pack` |
| `--sample` | Sample name written to the VCF |
| `--gbz` | Restrict calls to alleles present in the GBZ graph |

---

### 4.9 Final Output Files

For each srWGS sample, the final output files are:

| File | Description |
|------|-------------|
| `${SAMPLE}_sampled.pangenome.gbz` | Sample-specific haplotype-sampled pangenome graph |
| `${SAMPLE}_sampled.pangenome.gbz.snarls` | Snarl decomposition of the sampled graph |
| `${SAMPLE}.srWGS.pangenome_hapl.gam` | Graph alignment file |
| `${SAMPLE}.srWGS.pangenome_hapl.gam.log` | Mapping log file |
| `${SAMPLE}.srWGS.pangenome_hapl.gam.stats.txt` | Mapping statistics |
| `${SAMPLE}.srWGS.pangenome_hapl.gam.pack` | Read support file for variant calling |
| `${SAMPLE}_sampled.pangenome.chm13v2.vcf` | Variant calls on CHM13 coordinates |
| `${SAMPLE}_sampled.pangenome.grch38.vcf` | Variant calls on GRCh38 coordinates |

---

### 4.10 Complete Example Script

The following script performs the complete workflow for multiple srWGS samples.

```bash
#!/usr/bin/env bash
set -euo pipefail

# ============================================================
# KPPD srWGS graph mapping and variant calling pipeline
# ============================================================

WORKING_DIR=$(pwd)

SAMPLES=(srWGS1 srWGS2)

GRAPH=kor132.chm13v2.gbz
HAPL=kor132.chm13v2.hapl

THREADS=100
MEMORY=128
KMER=29
MIN_MAPQ=5

for SAMPLE in ${SAMPLES[@]}
do
    echo "========================================"
    echo "[Sample] ${SAMPLE}"
    echo "========================================"

    READ1=${SAMPLE}_R1.fastq.gz
    READ2=${SAMPLE}_R2.fastq.gz

    FASTQ_LIST=${SAMPLE}.input_fastq_files.txt

    KMC_PREFIX=${SAMPLE}.srWGS
    KFF=${KMC_PREFIX}.kff

    GBZ=${SAMPLE}_sampled.pangenome.gbz
    SNARLS=${GBZ}.snarls

    GAM=${SAMPLE}.srWGS.pangenome_hapl.gam
    PACK=${GAM}.pack

    VCF_CHM13=${SAMPLE}_sampled.pangenome.chm13v2.vcf
    VCF_GRCH38=${SAMPLE}_sampled.pangenome.grch38.vcf

    echo "[1/6] Building KMC k-mer index"

    printf "%s\n%s\n" ${READ1} ${READ2} > ${FASTQ_LIST}

    kmc \
        -k${KMER} \
        -m${MEMORY} \
        -okff \
        -t${THREADS} \
        @${FASTQ_LIST} \
        ${KMC_PREFIX} \
        ${WORKING_DIR}

    echo "[2/6] Generating haplotype-sampled pangenome graph"

    vg haplotypes \
        --verbosity 2 \
        --threads ${THREADS} \
        --include-reference \
        --diploid-sampling \
        --haplotype-input ${HAPL} \
        --kmer-input ${KFF} \
        --gbz-output ${GBZ} \
        ${GRAPH}

    echo "[3/6] Computing snarls"

    vg snarls \
        --threads ${THREADS} \
        ${GBZ} \
        > ${SNARLS}

    echo "[4/6] Mapping srWGS reads with vg giraffe"

    vg giraffe \
        --progress \
        --threads ${THREADS} \
        --gbz-name ${GBZ} \
        --fastq-in ${READ1} \
        --fastq-in ${READ2} \
        > ${GAM} \
        2> ${GAM}.log

    vg stats \
        --threads ${THREADS} \
        --alignments ${GAM} \
        > ${GAM}.stats.txt

    echo "[5/6] Generating read support with vg pack"

    vg pack \
        --threads ${THREADS} \
        --xg ${GBZ} \
        --gam ${GAM} \
        --output ${PACK} \
        --min-mapq ${MIN_MAPQ}

    echo "[6/6] Calling variants on CHM13 coordinates"

    vg call \
        --threads ${THREADS} \
        --ref-sample "CHM13v2" \
        ${GBZ} \
        --genotype-snarls \
        --snarls ${SNARLS} \
        --pack ${PACK} \
        --sample ${SAMPLE} \
        --gbz \
        > ${VCF_CHM13}

    echo "[6/6] Calling variants on GRCh38 coordinates"

    vg call \
        --threads ${THREADS} \
        --ref-sample "GRCh38" \
        ${GBZ} \
        --genotype-snarls \
        --snarls ${SNARLS} \
        --pack ${PACK} \
        --sample ${SAMPLE} \
        --gbz \
        > ${VCF_GRCH38}

    echo "[Done] ${SAMPLE}"
done
```

---

## 5. Citation

If you use KPPD in your research, please cite:

**Korean Precision Pangenome Draft (KPPD), National Institute of Health, Republic of Korea.**

A preprint citation will be added after manuscript release.

---

## 6. Contact

For questions or collaboration inquiries:

**pangenomekorean@gmail.com**

Korean Pangenome Project
