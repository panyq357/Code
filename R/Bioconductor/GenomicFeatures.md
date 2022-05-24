[GenomicFeatures](https://bioconductor.org/packages/release/bioc/html/GenomicFeatures.html) 包可以生成 TxDb 对象，以供其他分析使用。

### 从 GFF 生成 TxD

生成 TxDb 对象
```R
# 用 EnsemblPlants 上的水稻 GFF3 文件生成 TxDb
os_txdb <- makeTxDbFromGFF(file = "http://ftp.ensemblgenomes.org/pub/plants/release-52/gff3/oryza_sativa/Oryza_sativa.IRGSP-1.0.52.gff3.gz")
```

保存 TxDb 对象至一个 sqlite 文件

```
saveDb(os_txdb, file="resources/os_txdb.sqlite")
```