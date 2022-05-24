[ADMIXTURE](https://dalexander.github.io/admixture/) 是一个用于分析群体结构的软件，有着使用简单，分析速度快的特点。

ADMIXTURE 的命令很简单，只需要两个参数：基因型文件和 K 值。

```bash
admixture --cv my_snp.bed 2
```

通过添加 ``--cv`` flag，可以计算 CV error，比较不同 K 值的 CV error，好的 K 值的 CV error 会比较小。

在执行 admixture 之前，可先用 PLINK 的 ``--indep-pairwise`` 参数对 SNP 数据进行过滤，以降低计算量。

用 GNU parallel 可以同时跑多个 K 值。

```
seq 1 10 | parallel --cv 'echo {} | admixture mysnp.bed {.} > admixture_{.}.log'
```