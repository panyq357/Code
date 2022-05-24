clusterProfiler 是一个用于进行 GO、KEGG 等富集分析的软件。具体的软件文档可参考 [Y 叔写的书](https://yulab-smu.top/biomedical-knowledge-mining-book/index.html)。

clusterProfiler 的 `groupGO`、`enrichGO`、`gseGO` 等函数可以通过设置参数的方式，直接从 Biocunductor 的 OrgDb 包读取注释信息进行富集分析。

对于没有 OrgDB 的物种（比如水稻），则可手动将注释信息读进 R，然后使用 `enricher` 和 `GSEA` 函数进行富集分析。

## 栗子
### 水稻 GO 富集分析


## 参考
- [use clusterProfiler as an universal enrichment analysis tool](http://guangchuangyu.github.io/2015/05/use-clusterprofiler-as-an-universal-enrichment-analysis-tool/)
- [Selection Of Background Gene Set In Enrichment Analysis](https://www.biostars.org/p/17628/)