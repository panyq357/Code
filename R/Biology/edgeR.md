---
title: edgeR
tags:
    - Bioconductor
    - RNA-seq
---


## 栗子
### DGEList
edgeR 将数据都储存在一个基于 R 语言 list 的对象 —— DGEList 中。该对象可通过 `DGEList` 函数生成。

函数的参数：
- `counts`：counts matrix（不要进行正态化等预处理）
- `group`：样本分组的 factor，将被添加进 samples data.frame 中
- `genes`：基因或基因组区间注释的 data.frame
- `samples`：样本相关信息的 data.frame，其中包含一列 `lib.size`（如未提供该参数，将自动计算生成）

下面这段代码将从 Rsubread 的 featureCounts 函数得到的 fc 对象，构建成 DGEList。

```r
colnames(fc$counts) <- sub(".bam", "", colnames(fc$counts))

y <- DGEList(
    counts = fc$counts,
    group = sub("([^-]+)-.*", "\\1", colnames(fc$counts)),
    genes = fc$annotation[, "Length", drop=FALSE]  # Use drop=F to preserve data.frame structure
)
```

### Filter
对于 RNA-seq 来说，counts 数太低的 feature 通常应该被过滤掉。

可使用 `filterByExpr` 函数，或手动生成一个用于切片的布尔型向量，然后对 DGEList 进行切片即可进行过滤，其他元数据也将随着切片发生更改。

```r
keep <- filterByExpr(y)
keep <- rowSums(cpm(y) > 0.5) >= 2  # 手动

y <- y[keep, , keep.lib.sizes=FALSE]
```