---
title: biomaRt
tags:
    - Ensembl
    - Bioconductor
    - API
---

biomaRt 包

## 连接数据集

用 biomaRt 连接 Ensembl 中数据集的基本操作如下。
```R
# 载入包
library(biomaRt)
# 查看 Ensembl 提供哪些 biomart
listEnsembl()
# 调用 Ensembl 中名叫 gene 的 biomart
ensembl <- useEnsembl(biomart = "genes")
# 查看 biomart 中有哪些 dataset
listDatasets(ensembl)
# 查找有 hsapiens 字段的 dataset
searchDatasets(mart = ensembl, pattern = "hsapiens")
# 连接人类基因注视数据集 - 方法 1
ensembl_hsapiens <- useEnsembl(biomart = "genes", dataset = "hsapiens_gene_ensembl")
# 连接人类基因注视数据集 - 方法 2
ensembl_hsapiens <- useDataset(dataset = "hsapiens_gene_ensembl", mart = ensembl)
```

> 注：pattern 参数接受正则表达式

Ensembl 中是没有脊椎动物以外生物的数据的，要想获得水稻的注释信息，需要用另一套函数从 Ensembl Genomes 获取。

连接 Ensembl Genomes 中数据集的相关操作如下。
```R
# 查看 Ensembl Genomes 提供哪些 biomart
listEnsemblGenomes()
# 连接 Ensembl Plants 的 biomart
ensembl_plants <- useEnsemblGenomes(biomart = "plants_mart")
# 查找含有 IRGSP 字段的 dataset
searchDatasets(ensembl_plants, pattern = "IRGSP")
# 连接粳稻的基因注释数据集 - 方法 1
ensembl_osativa <- useEnsemblGenomes(biomart = "plants_mart", dataset = "osativa_eg_gene")
# 连接粳稻的基因注释数据集 - 方法 2
ensembl_osativa <- useDataset(dataset = "osativa_eg_gene", mart = ensembl_plants)

```

## 查询数据

查询数据使用的是 `getBM()` 函数。该函数需要三个参数：`filters`、`values` 和 `attributes`。

##### `filters` 相关操作
```R
# 列出 filters
listFilters(ensembl_osativa)
# 查找 filters（pattern 接受正则表达式）
searchFilters(mart = ensembl_osativa, pattern = "ensembl.*id")
# 列出一个 filter 接受选项（仅对部分 filter 有效，如染色体编号）
listFilterOptions(mart = ensembl_osativa, filter = "chromosome_name")
# 查找 filter 的选项
searchFilterOptions(mart = ensembl_osativa, filter = "biotype", pattern = "RNA")
```

##### `attributes` 相关操作
```R
# 列出数据集的 attributes
listAttributes(ensembl_osativa)
# 查找数据集的 filter 和 attributes
searchAttributes(mart = ensembl_osativa, pattern = "ensembl_gene_id")
```

##### 用 `select()` 查询数据
```R
AnnotationDbi::select(
  ensembl_osativa,
  keys = c("Os05g0113900"),
  keytype = "ensembl_gene_id",
  columns = c("entrezgene_id", "description")
)
```

 > ⚠️：若要不加 `AnnotationDbi` 包名直接使用 `select()` 函数，则需注意是否调用的是 `dplyr` 包中的同名函数。
 > ⚠️：可使用 `detach("package:dplyr", unload=TRUE)` 取消挂载 `dplyr` 包。


