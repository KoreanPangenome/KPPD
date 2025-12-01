# Telomere-to-Telomere Korean Pangenome Project  
## Dataset Structure & Data Dictionary (Draft)

**Last updated:** 2025-11-27  
**Status:** Draft (for AWS Open Data Onboarding)

---

## 📌 Table of Contents
1. [Overview](#1-overview)  
2. [Dataset Structure](#2-dataset-structure-draft)  
3. [File Types](#3-file-types)  
4. [File Naming Convention](#4-file-naming-convention-draft)  
5. [Sample Metadata](#5-sample-metadata-draft)  
6. [Release Plan & Versioning](#6-release-plan--versioning)  
7. [Future Additions](#7-future-additions)  
8. [Contact](#8-contact)

---

## 1. Overview

This document describes the structure, organization, and file types of the **Telomere-to-Telomere Korean Pangenome Project (KPP)** dataset.

The dataset includes:

- long-read sequencing data  
- telomere-to-telomere (T2T) assemblies  
- phased diploid assemblies  
- graph-based pangenome representations  
- variant datasets (SNPs, INDELs, SVs)  
- sample-level metadata  

This documentation helps users understand:

- folder structure  
- file naming conventions  
- metadata schema  
- data dictionary for annotations  
- locations of FASTQ, FASTA, VCF, GFA, and VG files  

This document will be updated once the AWS S3 bucket is provisioned.

---

## 2. Dataset Structure (Draft)

The dataset will follow a consistent directory structure after deployment.

/reads/
/ont_ul/
sample_id.ont.ul.fastq.gz
/hifi/
sample_id.hifi.fastq.gz
/hic/
sample_id.hic.fastq.gz
/ubam/
sample_id.ubam

/assemblies/
/t2t_fasta/
sample_id.t2t.fasta.gz
/t2t_gfa/
sample_id.t2t.gfa.gz
/diploid/
sample_id.hap1.fasta.gz
sample_id.hap2.fasta.gz

/variants/
/vcf/
sample_id.phased.sv.vcf.gz
sample_id.phased.snps.vcf.gz
/graph/
sample_id.vg
sample_id.gbwt
sample_id.giraffe.index

/metadata/
sample_metadata.csv
sequencing_summary.json

/docs/
version_history.md
qc_summary.md

> **Note:** Final structure may be updated to align with AWS bucket guidelines.

---

## 3. File Types

| File Type | Description | Notes |
|-----------|-------------|-------|
| **FASTQ** | Raw ONT ultra-long or PacBio HiFi reads | gzip-compressed |
| **uBAM** | Unaligned BAM files | Includes per-read metadata |
| **FASTA** | Genome assemblies (T2T or haplotype) | Files can exceed 3 Gb |
| **GFA** | Assembly graph files | Standard for T2T assemblies |
| **VCF** | SNP/INDEL/SV calls | Provided with `.tbi` index |
| **VG** | Graph genome representation | Compatible with VG toolkit |
| **CSV/JSON** | Sample metadata | Detailed schema to be updated |

---

## 4. File Naming Convention (Draft)

KPP####.ont.ul.fastq.gz
KPP####.hifi.fastq.gz
KPP####.t2t.fasta.gz
KPP####.sv.vcf.gz
KPP####.vg

Where:

- `KPP####` = internal sample ID  
- suffix = data type & processing method  

This enables automation-friendly pipelines.

---

## 5. Sample Metadata (Draft)

`metadata/sample_metadata.csv` contains:

| Column | Description | Example |
|--------|-------------|---------|
| **sample_id** | Internal sample identifier | KPP0123 |
| **sequencing_platform** | ONT UL / PacBio HiFi / Hi-C | PacBio HiFi |
| **mean_read_length** | Average read length | 18,600 |
| **coverage** | Estimated genome coverage | 35x |
| **sex** | Male/Female | Female |
| **population** | Population label | Korean |
| **batch** | Sequencing batch | HIFI_2025_01 |

A complete schema will be added after QC.

---

## 6. Release Plan & Versioning

- **Initial release:** v1.0 (2025)  
- **Expected growth:** ~350 TB/year  
- Planned supporting documents:  
  - `docs/version_history.md`  
  - `docs/qc_summary.md`  
  - `docs/file_index.csv`  

---

## 7. Future Additions

The following will be included after AWS provisioning:

- final S3 bucket name & region  
- exact file paths  
- expanded metadata schema  
- examples for `aws s3`, `awscli`, `s3fs`  
- documentation for graph genome indexing  

---

## 8. Contact

For questions or collaboration:

📧 **inthistime@korea.kr**  
National Institute of Health, Republic of Korea

---


