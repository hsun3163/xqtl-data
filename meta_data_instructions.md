# Contributing to the data descriptor document

The specification for meta-data descriptor was developed by Xuanhe Chen and Gao Wang, to incorporate and extend information required by NIAGADS for the FunGen-xQTL resource release.
Please contact Gao if you have any issues or concerns with this mechanism.

## How to complete the descriptor for the data-set you analyzed?

### Overview of the organization of meta-data files

Under `data` folder, we have these key directories:

```
├── descriptor
│   ├── gwas
│   ├── integration
│   ├── omics
│   ├── qtl
│   ├── study_info
├── MiGA
├── NIAGADS
├── ROSMAP
├── STARNET
├── template
```

1. `descriptor` and `template` are what you need to contribute with the meta-data information. 
2. `NIGADS` folder contains the meta-data in xlsx format that NIAGADS requires for submission to NIAGADS.
3. Folders with study names, such as `ROSMAP`, `MiGA`, `STARNET`, contain supplementary meta-data you need to also provide for NIAGADS submission. Notice that **these must contain the exact subset of samples you used for the QTL mapping --- after QC filter and taking overlap with available genotype data**. For example:

```
├── MiGA
│   ├── MiGA_computational_protocol.csv
│   ├── MiGA_lab_protocol.csv
│   └── MiGA_sample_attributes.csv
```

The computational protocol CSV file should be generated by our QTL calling pipeline. Please contact Hao Sun if you have an issue getting the computational protocol CSV file. For format reference of the csvs please check `data/template/FGC_metadata_v5_Intructions+schema_v2_shared.xlsx`.

Under `data` folder, type `make`, a table of contents will be generated automatically to show the data-set we have, as this page: https://github.com/cumc/fungen-xqtl-analysis/tree/main/data

**Data-set with a red tick in front of analysts name indicates that this meta-data information has been complete, and was reviewed and edited by Gao Wang. When you believe you have completed your meta-data please pin Gao to review it.**

### Add your meta-data

For the completeness of an xQTL study, you will need to create:

1. Study information, under folder `data/descriptor/study_info`, based on template `template/study_descriptor.md`.
2. Molecular trait information, under folder `data/descriptor/omics`, based on template `template/omics_descriptor.md`.
3. QTL information, under folder `data/descriptor/qtl`, based on template `template/QTL_descriptor.md`
4. Complete the supplementary CSV meta-data files.

If you work with GWAS summary data fine-mapping and integration, you need to create:

1. GWAS summary statistics information, under folder `data/descriptor/gwas`, based on template `template/gwas_descriptor.md`

Example for the ROSMAP H3K9ac QTL study:

1. Study information: https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/descriptor/study_info/ROSMAP.md
2. Molecular trait information: https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/descriptor/omics/ROSMAP_DLPFC_ChIPSeq_H3K9ac.md
3. QTL information: https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/descriptor/qtl/ROSMAP_DLPFC_ChIPSeq_H3K9ac_qtl.md
4. Supplementary CSV:
    - https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/ROSMAP/ROSMAP_h3k9ac_sample_attributes.csv
    - https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/ROSMAP/ROSMAP_h3k9ac_lab_protocol.csv 
    - https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/ROSMAP/ROSMAP_h3k9ac_computational_protocol.csv

and a GWAS example:

- https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/template/gwas_descriptor.md

## Commands to export NIAGADS compatible meta-data

Please run these commands under `data` folder. You need to install `xlsxwriter` Python package in order to run the commands:

```bash
pip install xlsxwriter
```

**NIAGADS/ROSMAP_DLPFC_ChIPSeq_H3K9ac_qtl_metadata.xlsx**

```
sos run md_to_niagads.ipynb \
    --omics descriptor/omics/ROSMAP_DLPFC_ChIPSeq_H3K9ac.md \
    --qtl descriptor/qtl/ROSMAP_DLPFC_ChIPSeq_H3K9ac_qtl.md \
    --output_dir NIAGADS
```

**NIAGADS/ROSMAP_snRNAseq_pseudo_bulk_qtl_metadata.xlsx**

```
sos run md_to_niagads.ipynb \
    --omics descriptor/omics/ROSMAP_snRNAseq_pseudo_bulk.md \
    --qtl descriptor/qtl/ROSMAP_snRNAseq_pseudo_bulk_qtl.md \
    --output_dir NIAGADS
```

**NIAGADS/ROSMAP_DLPFC_expression_qtl_metadata.xlsx**

```
sos run md_to_niagads.ipynb \
    --omics descriptor/omics/ROSMAP_DLPFC_expression.md \
    --qtl descriptor/qtl/ROSMAP_DLPFC_expression_qtl.md \
    --output_dir NIAGADS
```

**NIAGADS/MiGA_brain_expression_qtl_metadata.xlsx**

```
sos run md_to_niagads.ipynb \
    --omics descriptor/omics/MiGA_brain_expression.md \
    --qtl descriptor/qtl/MiGA_brain_expression_qtl.md \
    --output_dir NIAGADS
```

**NIAGADS/STARNET_macrophage_qtl_metadata.xlsx**

```
sos run md_to_niagads.ipynb \
    --omics descriptor/omics/STARNET_macrophage.md \
    --qtl descriptor/qtl/STARNET_macrophage_qtl.md \
    --output_dir NIAGADS
```

## Upload to xQTL FTP server

To upload meta-data (and other files) to the xQTL FTP server please see [this tutorial](https://github.com/cumc/fungen-xqtl-analysis/blob/main/data/Example_FTP_File_Transfer.ipynb) created by Travyse Edwards (MSSM).