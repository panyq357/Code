[ChIPseeker](https://bioconductor.org/packages/release/bioc/html/ChIPseeker.html) 是一个处于 ChIP-seq 分析下游，对 peaks 提供注释，以及可视化的包。

`annotatePeak` ： ChIPseeker 包中用于注释 peaks 的函数
- 输入
	- 基因组位置信息 GRanges
	- 基因组注释信息 TxDb（TxDb 对象可由 [[GenomicFeatures]] 包生成）
- 输出：带有注释的 GRanges

以下是一个例子：

```R
r$> all(levels(my_peaks@seqnames) %in% my_txdb$user_seqlevels)
[1] TRUE

r$> my_anno <- annotatePeak(peak = my_peak, TxDb = my_txdb)
>> preparing features information...             2022-03-18 18:23:40
>> identifying nearest features...               2022-03-18 18:23:40
>> calculating distance from peak to TSS...      2022-03-18 18:23:41
>> assigning genomic annotation...               2022-03-18 18:23:41
>> assigning chromosome lengths                  2022-03-18 18:23:42
>> done...                                       2022-03-18 18:23:42

```

> 注意⚠️：GRanges 的 seqnames 的 Levels 和 TxDb 的 user_seqlevels 需要一致，否则会报错。