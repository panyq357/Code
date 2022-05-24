---
tags:
    - Bioinformatics
    - Sequence Alignment
---

`bwa` 是一个用于将测序得到的 `.fastq` 文件比对到参考基因组上，获得比对结果 `.sam` 的软件。

## bwa index
`bwa index` 命令用于对参考基因组建索引。

```
bwa index -p my_index ref.fa
```

- `-p`：生成索引文件的前缀，不加的话就和 fasta 文件同名

## bwa mem
`bwa mem` 命令用于使用 “maximum exact matches” 算法进行序列比对。

- `-t`：线程数
- `-M`：当存在多个比对结果时，将较短的比对结果标记为“次优”，这是为了与 Picard 兼容。
- `-P`：
- `-R`：设置表头，用于在后续合并比对结果时区分来自不同批次的比对结果。
	- `@RG`：（Read groups）表头开始的固定字符
	- `ID` ：（Read group identifier）样品 ID
	- `PU`：（Platform Unit）测序样品在测序机器中的的信息
	- `SM`：（Sample）样品信息
	- `PL`：（Platform/technology used to produce the read）测序平台信息
	- `LB`：（DNA preparation library identifier）


## 参考
- [bwa.1 (sourceforge.net)](http://bio-bwa.sourceforge.net/bwa.shtml)：bwa 的文档
- [Read groups – GATK (broadinstitute.org)](https://gatk.broadinstitute.org/hc/en-us/articles/360035890671-Read-groups)：GATK 文档中关于序列表头的详细说明