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

### 2.1 Long-Read Assembly
- **ONT Ultra-long reads**: basecalling → adapter trimming → QC  
- **PacBio HiFi reads**: CCS generation → filtering → QC  
- Assemblers used: **hifiasm**, **hifiasm-t2t**, ONT-aware polishing  
- Haplotypes generated using hifiasm phasing  
- Manual curation performed for T2T samples

### 2.2 Pangenome Graph Construction
- Backbone reference: **T2T-CHM13 v2.0**  
- Tools used:  
  - **Minigraph-Cactus** for multi-assembly graph  
  - **VG toolkit** for GBZ graph generation (`vg gbwt`, `vg index`, `vg giraffe`)

### 2.3 Variant Calling
- SV calling from assemblies using:  
  - **PAV2** / **SVP**  
  - **WAVE** for assembly-aware SV merging  
- SNP/INDEL processing coordinated to CHM13; GRCh38 versions also generated

### 2.4 Output Files
- Multi-assembly graph (GFA, GBZ)  
- Population haplotype panel  
- SV / SNP / INDEL variation sets  
- QC metrics and MD5 checksums  

---

## 3. Data Links

The following dataset files are available via Google Drive.

| Filename | Description | Link |
|----------|-------------|------|
| **kor132.chm13v2.gfa.gz** | Multi-assembly pangenome graph (GFA) | [Download](https://drive.google.com/file/d/1aG5d70RsDNPzGBim7Tax-cDtG1dmAQdY/view?usp=drive_link) |
| **kor132.chm13v2.gbz** | GBZ-format graph (VG-compatible) | [Download](https://drive.google.com/file/d/1y84nTxuCevpvNlsO8KyDGiV7RyzI2O59/view?usp=drive_link) |
| **kor132.chm13v2.hapl** | Population haplotype panel | [Download](https://drive.google.com/file/d/1cwrrG7F0Xupi2S2UpN8KMNFDSzYPrH5z/view?usp=drive_link) |
| **kor132.chm13v2.sv.gfa.fa.gz** | SV graph (GFA + FASTA) | [Download](https://drive.google.com/file/d/10JfxoOObxcJD2HqAdiXeuAJeI0GY9y06/view?usp=drive_link) |
| **kor132.chm13v2.wave.vcf.gz** | SV calls (CHM13 coordinates) | [Download](https://drive.google.com/file/d/1IsVE6usKf58DJzXshVrk8-GlmYdUMxsU/view?usp=drive_link) |
| **kor132.chm13v2.GRCh38.wave.vcf.gz** | SV calls lifted to GRCh38 | [Download](https://drive.google.com/file/d/1QBOxyrVRvJASzgJ-pDh0Z-1MY1wi-r5C/view?usp=drive_link) |
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
