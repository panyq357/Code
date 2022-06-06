clusterProfiler 是一个用于进行 GO、KEGG 等富集分析的软件。具体的软件文档可参考 [Y 叔写的书](https://yulab-smu.top/biomedical-knowledge-mining-book/index.html)。

clusterProfiler 的 `groupGO`、`enrichGO`、`gseGO` 等函数可以通过设置参数的方式，直接从 Biocunductor 的 OrgDb 包读取注释信息进行富集分析。

对于没有 OrgDB 的物种（比如水稻），可从 biomaRt 获得注释，然后使用 `enricher` 和 `GSEA` 函数进行富集分析。

## 栗子
### 水稻 GO 富集分析
```r
gene_vector <- "Os11g0559200"

# 从 biomaRt 上获取注释
library(biomaRt)
ensembl_osativa <- useEnsemblGenomes(
    biomart = "plants_mart",
    dataset = "osativa_eg_gene"
)
bm_result <- getBM(
    attribute=c("ensembl_gene_id", "go_id", "name_1006"),
    filters="ensembl_gene_id",
    values=gene_vector,
    mart=ensembl_osativa
)


```

### 水稻


## 参考
- [use clusterProfiler as an universal enrichment analysis tool](http://guangchuangyu.github.io/2015/05/use-clusterprofiler-as-an-universal-enrichment-analysis-tool/)
- [Selection Of Background Gene Set In Enrichment Analysis](https://www.biostars.org/p/17628/)