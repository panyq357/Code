
[snpStats 的 bioconductor 页面](https://bioconductor.org/packages/release/bioc/html/snpStats.html)

### 安装

```R
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("snpStats")
```

### 读取 PLINK 数据（`.bed`, `.bim`, `.fam`）

```R
my_plink_data <- read.plink(bed = "my_plink_data.bed",
		                    bim = "my_plink_data.bim",
		                    fam = "my_plink_data.fam")
```

这里读进来的 `my_plink_data` 是一个 `list`，里面有三个元素：`genotypes`，`fam`，`map`。

```R
> class(my_plink_data)
[1] "list"
> names(my_plink_data)
[1] "genotypes" "fam"       "map"
```

- `genotypes` 为一个 `SnpMatrix`，储存着 SNP 数据。
- `fam` 为每个个体的家系和表型信息。
- `map` 为 SNP 位置信息，其中 `allele.1` 列对应 VCF 中的 ALT，`allele.2` 列对应 VCF 中的 REF。

SnpMatrix 中基因型数字对应的含义如下表

| SnpMatrix | VCF | Genotype |
|:---------:|:---:|:--------:|
|    03     | 0/0 | Homo Ref |
|    01     | 1/1 | Homo Alt |
|    02     | 0/1 |  Hetero  |
|    00     | ./. | Missing  |

以下是一个从 `read.plink` 生成的 `list` 中读取指定 SNP 的基因型信息的函数，函数返回一个长列表，每一行是一个个体，第一列为个体 ID，第二列为表型数值，第三列为对应 SNP 位点的基因型。

```R
get_snp_long <- function(plink, chr, pos) {
    snp_name <- plink$map %>% filter(chromosome == chr, position == pos) %>% pull(snp.name) %>% as.character()
    snp_genotype <- plink$genotypes[,snp_name] %>% as.data.frame()
    snp_info <- plink$map[snp_name,]
    snp_long <- data.frame(ID = plink$fam$member, Value = plink$fam$affected, Alleles = NA)
    snp_long[snp_genotype[,1] == 03, "Alleles"] <- str_c(snp_info$allele.2, "/", snp_info$allele.2)
    snp_long[snp_genotype[,1] == 01, "Alleles"] <- str_c(snp_info$allele.1, "/", snp_info$allele.1)
    snp_long[snp_genotype[,1] == 02, "Alleles"] <- str_c(snp_info$allele.1, "/", snp_info$allele.2)
    snp_long[snp_genotype[,1] == 00, "Alleles"] <- "missing"
    return(snp_long)
}
```