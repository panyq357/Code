
## 构建 DGEList
下面这段代码将从 Rsubread 的 featureCounts 函数得到的 fc 对象，构建成 DGEList。

```r
# fc variable in this RData image was the result from featureCount pipeline
load("results/featureCount/saved_image.RData")

colnames(fc$counts) <- sub(".bam", "", colnames(fc$counts))

y <- DGEList(
    counts = fc$counts,
    group = sub("([^-]+)-.*", "\\1", colnames(fc$counts)),
    genes = fc$annotation[, "Length", drop=FALSE]  # Use drop=F to preserve data.frame structure
)
```

## 根据 CPM 筛选基因

```r
keep <- rowSums(cpm(y) > 0.5) >= 2
y <- y[keep, , keep.lib.sizes=FALSE]
```