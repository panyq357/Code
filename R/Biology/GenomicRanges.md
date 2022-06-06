[GenomicRanges](https://bioconductor.org/packages/release/bioc/html/GenomicRanges.html) 是 Bioconductor 中的提供基础设施的包。它提供了一系列用于操纵基因组区间的函数。

## _GRanges_

_GRanges_ 类是一个用于储存基因组区间数据的类，构建一个 _GRanges_ 对象的示例如下。

```R
gr <- GRanges(
	seqnames = Rle(c("chr1", "chr2", "chr1", "chr3"),c(1, 3, 2, 4)),
	ranges = IRanges(start=101:110, end=111:120, names=head(letters, 10)),
	strand = Rle(strand(c("-", "+", "*", "+", "-")), c(1, 2, 2, 3, 2)),
	score = 1:10,
	GC = seq(1, 0, length=10))
```

- `seqnames`：染色体或 contig 名
- `ranges`：染色体上的物理位置
- `strand`：在染色体的朝向：正链（`+`）、反链（`-`）或未知（`*`）

### 集合运算
*GRanges* 类支持集合的运算。

使用 `subsetByOverlaps` 函数取交集便可获得指定位置的 GRanges 子集。
```R
start <- 3985647 - 2000
end <- 3994398 + 1000

gff <- rtracklayer::import("rawdata/gff_RAP2/all.gff")
gene_info <- gff %>% subsetByOverlaps(GRanges(seqnames = "chr1", ranges = IRanges(start=start, end=end)))
```

## 参考
- [How do I subset a GRanges on chromosome, region and strand?](https://www.biostars.org/p/351377/#351383)：用 `subsetByOverlaps` 函数提取 GRanges 子集