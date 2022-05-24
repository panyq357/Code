---
title: Ensembl Variant Effect Predictor (VEP)
author: panyq
tags:
    Ensembl
    CommandLine
    VCF
    Annotation
---

VEP 是 Ensembl 出品的注释 SNP 的工具。[^1]

## 安装

Ensembl 上的 VEP 安装教程比较繁琐，而 bioconda 上提供了一个开箱即用的版本，使用 conda 即可安装。[^2]

```bash
mamba install ensembl-vep
```

## 栗子
一个用 GFF 文件对 VCF 进行注释，并输出 bgzip 压缩的 VCF 文件的例子如下。

首先需要对 GFF 文件进行排序，并用 bgzip 压缩，用 tabix 建索引。

```bash
zcat < anno.gff.gz \
    grep -v '^#' \
    sort -k1,1 -k4,4n -k5,5n -t$'\\t' \
    bgzip -c > anno_sorted_bgzip.gff.gz \
tabix -p gff anno_sorted_bgzip.gff.gz
```

然后便可用 vep 进行注释了。

```bash
vep --vcf \
    --input_file genotype.vcf.gz \
    --gff anno_sorted_bgzip.gff.gz \
    --fasta ref_genome.fa.gz \
    --compress_output bgzip \
    --fields "Consequence,Gene,Amino_acid_change" \
    --output_file output.vcf.gz \
    --stats_file output_annotation_summary.html
```

参数含义如下。[^3]
- `--vcf`：以 VCF 格式输出
- `--gff`：注释 GFF
- `--fasta`：参考基因组 FASTA
- `--compress_output`：压缩格式，可选 `bgzip` 和 `gzip`
- `--fields`：注释的具体内容，详见文档说明[^4]。

在程序运行结束后，新生成的 VCF 的 INFO 列中将新增一个名为 CSQ 的键值对，这就是 VEP 加的注释了。[^5]


[^1]: [Ensembl Variant Effect Predictor (VEP)](https://asia.ensembl.org/info/docs/tools/vep/index.html)
[^2]: [Package Recipe 'ensembl-vep'](https://bioconda.github.io/recipes/ensembl-vep/README.html)
[^3]: [Variant Effect Predictor - Running VEP](https://asia.ensembl.org/info/docs/tools/vep/script/vep_options.html)
[^4]: [output columns](https://asia.ensembl.org/info/docs/tools/vep/vep_formats.html#output)
[^5]: [VCF output](https://asia.ensembl.org/info/docs/tools/vep/vep_formats.html#vcfout)