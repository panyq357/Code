[LDheatmap](https://sfustatgen.github.io/LDheatmap/index.html) 是一个用于绘制一段区间内的 SNP 连锁关系的热图的 R 包。

> 有类似功能的软件还有 [LDBlockShow](https://doi.org/10.1093/bib/bbaa227)，[snp.plotter](https://doi.org/10.1093/bioinformatics/btl657)，[IntAssoPlot](https://doi.org/10.3389/fgene.2020.00260)等。

## 软件安装
LDheatmap 的软件本体是在 CRAN 上的，但它的一系列依赖都是 Bioconductor 上的，得先手动安装。

```bash
mamba install \
    r-devtools \
    bioconductor-snpstats \
    bioconductor-rtracklayer \
    bioconductor-GenomicRanges \
    bioconductor-GenomInfoDb \
    bioconductor-IRanges
```

然后再安装 LDheatmap（conda 上没有 LDheatmap）。

```r
devtools::install_github("SFUStatgen/LDheatmap")
```

## 栗子
```r
data(CEUDist)
data(CEUSNP)
LDheatmap(
    CEUSNP,
    CEUDist,
    LDmeasure="r",
    title="Pairwise LD in r^2",
    add.map=TRUE,
    SNP.name=c("rs2283092", "rs6979287"),
    heat.colors(20),
    name="myLDgrob",
    flip=TRUE,
    add.key=TRUE
)
```