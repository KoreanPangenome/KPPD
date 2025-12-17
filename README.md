# A Draft Korean Pangenome Reference: KPPD
**Last updated:** 2025-12-09  
**Status:** Draft Release  

---
## Table of Contents
1. [Overview](#1-overview)  
2. [Analysis Workflow](#2-analysis-workflow)  
3. [Data Downloads](#3-data-downloads)  
4. [Citation](#4-citation)  
5. [Contact](#5-contact)
---

## 1. Overview

**A Draft Korean Pangenome Referenc (KPPD)** is a population-scale Korean pangenome reference constructed from **132 deep-sequenced Korean individuals**.  
The dataset integrates telomere-to-telomere assemblies and high-quality long-read assemblies to enable accurate structural variant discovery, genome graph construction, and haplotype resolution.

### Composition of the Dataset

| Category | Individuals | Sequencing | Notes |
|---------|-------------|------------|-------|
| **T2T-level assemblies** | 4 | PacBio Revio 60×, ONT Ultra-Long 60×, Omni-C (300M read pairs) | Full telomere-to-telomere resolution |
| **Non-T2T long-read assemblies** | 128 | PacBio Revio ~30× | High-contiguity diploid assemblies |

**Total:** 132 Korean genomes were used to construct the pangenome graph and variant catalogue.

---

## 2. Analysis Workflow

The Korean Pangenome Draft (KPPD) was constructed through a multi-stage workflow integrating long-read assemblies, graph construction, and haplotype-aware read alignment. Below is the summary of the full analysis pipeline.

---

### 2.1 Sequencing Data Generation

A total of **132 genomes** were sequenced:

- **128 PacBio Revio HiFi datasets**  
  - ~30× depth, N50 ~16 kb, Q28 median
- **4 T2T-level datasets**  
  - PacBio Revio HiFi (~60×)  
  - ONT Ultra-Long (~60×; N50 ~90 kb)  
  - Dovetail Omni-C (40×, 151 bp)

These datasets were used to generate high-quality haplotype-resolved assemblies.

---

### 2.2 Assembly Construction (Hifiasm)

Assemblies were constructed using:

**Hifiasm (v0.19.9–r616)**

- **For 128 non-T2T samples:**  
  - Hifiasm produced *partial phased contigs per sample* (Hap1 / Hap2)
  - Total: 256 raw assemblies

- **For 4 T2T samples:**  
  - Hifiasm generated *fully phased T2T-level haplotype assemblies*
  - Total: 8 raw assemblies

Resulting assemblies included both partially phased and fully phased haplotype contigs depending on sequencing depth.

---

### 2.3 Assembly Correction

Raw assemblies were polished and corrected through the following steps:

- **Error correction using self-alignment of PacBio HiFi reads**  
  Tool: **Inspector v1.3.1**
- **Final output: 264 corrected assemblies**  
  - HiFi-only genomes:  
    - Mean: 561 contigs, QV ~53  
  - T2T-level haplotypes:  
    - Mean: 102 contigs, QV ~54

Corrected haplotypes were used as input for graph construction.

---

### 2.4 Draft Korean Pangenome Graph Construction

The **Draft Korean Pangenome Graph** was built using:

- **Minigraph-cactus (v2.9.3) ** for multi-assembly genome graph construction
  - Input references:  
    - CHM13 v2.0  
    - GRCh38  
    - 132 Korean haplotype assemblies  
  - Output graph size:  
    - **123 M nodes, 171 M edges, 3.45 GB (GBZ/GFA)**

This graph represents the merged Korean haplotype diversity on the CHM13 backbone.

---

### 2.5 Haplotype-Aware Short-Read Alignment

Short reads were aligned to the pangenome graph using:

- **vg giraffe (v1.6.7)** for haplotype-aware mapping  
- Alignment output: **GAM format**

A haplotype depth filter was applied using:

- **vg clip (1.6.7)**

Filtering thresholds:

- HPRC haplotypes with >9× depth (AF > 0.1)  
- Korean pangenome haplotypes with >2× depth (AF > 0.01)  
- Korean haplotypes with >53× depth (AF > 0.2)

These filters refine haplotype representation for variant interpretation.

---

## 3. Data Links

The following dataset files are available via Google Drive.

| Filename | Description | Link |
|----------|-------------|------|
| **kor132.chm13v2.gfa.gz** | Multi-assembly pangenome graph (GFA) | [Download](https://drive.google.com/file/d/1aG5d70RsDNPzGBim7Tax-cDtG1dmAQdY/view?usp=drive_link) |
| **kor132.chm13v2.gbz** | GBZ-format graph (VG-compatible) | [Download](https://drive.google.com/file/d/1y84nTxuCevpvNlsO8KyDGiV7RyzI2O59/view?usp=drive_link) |
| **kor132.chm13v2.hapl** | Population haplotype panel | [Download](https://drive.google.com/file/d/1cwrrG7F0Xupi2S2UpN8KMNFDSzYPrH5z/view?usp=drive_link) |
| **kor132.chm13v2.sv.gfa.fa.gz** | SV graph (GFA + FASTA) | [Download](https://drive.google.com/file/d/1OLH_PjftZO6KIXXAC4aqtc49Quk3agX5/view?usp=drive_link) |
| **kor132.chm13v2.wave.vcf.gz** | VCF INFO (CHM13 coorrdinates) | [Download](https://drive.google.com/file/d/1o2kNQdoMR2y5AvXgoS3yUNmVYVNMtMEO/view?usp=drive_link) |
| **kor132.chm13v2.GRCh38.wave.vcf.gz** | VCF INFO (GRCh38 coorrdinates) | [Download](https://drive.google.com/file/d/1_FqGHXKGGB1fnmQt7sVndiSMXbHTAZz_/view?usp=drive_link) |
| **upload_md5sum.txt** | MD5 checksum file | [Download](https://drive.google.com/file/d/1KhzOZ15xamKJ9ceK356ZBKf0_kMWaZuV/view?usp=drive_link) |

---


## 4. Citation

If you use KPPD in your research, please cite:

**(Not yet) Korean Precision Pangenome Draft (KPPD), National Institute of Health, Republic of Korea (2025).**  

A preprint citation will be added after manuscript release.

---

## Contact

For questions or collaboration inquiries:  
**pangenomekorean@gmail.com**  
Korean Pangenome Project
