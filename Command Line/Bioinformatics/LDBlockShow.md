---
tags: 
    - LDheatmap
    - CommandLine
    - GWAS
---
[LDBlockShow](https://github.com/hewm2008/LDBlockShow) 是一个快速的 LD 热图绘制工具。

PMID: [33126247](https://pubmed.ncbi.nlm.nih.gov/33126247)   DOI:[10.1093/bib/bbaa227](https://doi.org/10.1093/bib/bbaa227)

## 安装
**注意**：虽然 bioconda 里有 ldblockshow 这个软件包，但由于 LDBlockShow 需要调用一些外部的模块（比如 SVG.pm），而这些模块的调用路径好像是 hard-coded 的相对于 LDBlockShow 的可执行文件的相对路径，所以只用 conda 安装的话，会缺少依赖，想补依赖也很麻烦。

所以只能从 github 上下载软件包了。

```bash
git clone https://github.com/hewm2008/LDBlockShow.git
cd LDBlockShow ; chmod 755 configure ; ./configure
make
mv LDBlockShow bin/ ; rm *.o
cd ..
```

## 栗子
**注意**：虽然 LDBlockshow 提供 -Region 选项，但它提取出区间内的 SNP 的方式似乎是通过用 awk 命令从头到尾扫一遍。所以用 tabix 把 vcf 先准备好，能极大的加快绘图速度。

```bash
mkdir -p results/ldblockshow

FILEPATH="resources/snpeff/NB_final_snp.vcf.gz"
REGION="9:16682867-17688315"

LDBlockShow/bin/LDBlockShow \
    -InVCF <(tabix -H ${FILEPATH}; tabix ${FILEPATH} ${REGION}) \
    -OutPut results/ldblockshow/${REGION}_ldheatmap \
    -Region ${REGION} \
    -OutPng \
    -NoShowLDist 999999999
```