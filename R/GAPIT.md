[GAPIT](https://zzlab.net/GAPIT/) 是一个用于进行 GWAS 的 R 包，包含了众多模型。

## 安装依赖
GAPIT 的软件本体就是一个单一的 R 脚本，所以相关的依赖都得自己安装（而且 GAPIT 的软件文档中写的不全，都靠报错提示缺哪些包😥）。

```R
# Use TUNA mirror
options("repos" = c(CRAN="https://mirrors.tuna.tsinghua.edu.cn/CRAN/"))

# GAPIT3 dependencies for GLM, CMLM, BLINK
install.packages("gplots")
install.packages("genetics")
install.packages("ape")
install.packages("EMMREML")
install.packages("scatterplot3d")
install.packages("BiocManager")
BiocManager::install("snpStats")
BiocManager::install("multtest")
install.packages("LDheatmap")
install.packages("plotly")
install.packages("bigmemory")
```


## Hapmap 格式

GAPIT 所需的输入文件为与 [[TASSEL]] 通用的 Hapmap 格式。

Hapmap 文件的前 11 列为 SNP 的一些元数据。其中，只有 `rs`、`chrom` 和 `pos` 列为 GAPIT 真正会使用的列，其余的都可以设为 `NA`。

```txt
rs#     alleles chrom   pos     strand  assembly#       center  protLSID        assayLSID       panelLSID       QCcode  B001
1151    C/A     1       1151    +       NA      NA      NA      NA      NA      NA      M       C       C       A       C
1178    G/T     1       1178    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
1203    T/C     1       1203    +       NA      NA      NA      NA      NA      NA      T       T       T       T       T
1248    G/A     1       1248    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
1282    G/A     1       1282    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
1299    T/C     1       1299    +       NA      NA      NA      NA      NA      NA      T       T       T       T       T
1306    G/A     1       1306    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
1335    G/T     1       1335    +       NA      NA      NA      NA      NA      NA      G       N       G       G       G
1792    G/A     1       1792    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
2226    G/A     1       2226    +       NA      NA      NA      NA      NA      NA      G       G       G       G       G
2599    C/T     1       2599    +       NA      NA      NA      NA      NA      NA      C       C       C       C       C
```

对于从第 12 列开始往后的各样本的基因型，GAPIT 支持用 IUPAC 单字母缩写来表示二倍体的基因型。

| Genotype | AA  | CC  | GG  | TT  | AG  | CT  | CG  | AT  | GT  | AC  |
| -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Code     | A   | C   | G   | T   | R   | Y   | S   | W   | K   | M   | 

对于缺失的基因型，双字母用 `NN` 表示，单字母用 `N` 表示。

## GAPIT
一个典型的用 GAPIT 进行 GWAS 的脚本如下所示。

```R
# Load GAPIT functions
source("scripts/gapit_functions.txt")

# Read-in phenotype data
pheno <- read.delim("rawdata/phenotype/grain_length.txt", head=FALSE)
colnames(pheno) <- c("Taxa", "GL")

# Read-in Hapmap file
hapmap <- read.delim("resources/gwas_snp.hmp.txt", head=FALSE)

# GAPIT GLM
dir.create("results/GL")
setwd("results/GL")
myGAPIT <- GAPIT(
    Y=pheno,
    G=hapmap,
    model=c("GLM", "CMLM", "Blink"),
    PCA.total=5,
    Inter.Plot=TRUE,
    Multiple_analysis=TRUE,
    file.output=T
)
setwd("../..")

```

### 一些坑
1. GAPIT 对输入数据非常挑剔，必须得是 r-base 的 data.frame，不能是 tidyverse 的 tibble，及其他类似的数据结构。
2. 在用 `read.delim` 函数读入 hapmap 文件时，必须使用 `head=FALSE` 参数，使读进来的 data.frame 的第一行为 hapmap 文件的表头。

### 调试
与其直接跑全部的数据，等很长时间，然后报错。不如先生成一个示例数据进行调试。
```bash
# 复制表头
head -n 1 all.hmp.txt > test.hmp.txt
# 随机挑选 1000 行
shuf -n 1000 all.hmp.txt >> test.hmp.txt
# 按染色体位置排个序
sort -nk 1,4 test.hmp.txt > test.sort.hmp.txt
```

### 报错及解决办法
1. `Y is empty`：这是由于 GAPIT 没法读取表型导致的，在表型数据为 tibble 而不是 data.frame 时会出现。