[tabix](http://www.htslib.org/doc/tabix.html) 是一个用于对常见的 SAM/BAM、VCF 等文件建索引的软件，以加快读取特定染色体位置数据的速度。

- `-p`：指定文件类型，可以是 gff、bed、sam、vcf
    - 如要对 GTF 进行处理，选 gff 就行（两种格式的位置信息的位置一样）
- `-H`：只输出表头
- `-h`：输出表头以及内容

在用 tabix 建索引之前，需要用其配套的 [bgzip](http://www.htslib.org/doc/bgzip.html) 对文件进行压缩。

## 栗子
首先，使用 bgzip 对 VCF 文件进行压缩（默认会删除原文件），然后用 tabix 对压缩后的文件建索引。

```zsh
bgzip resources/pruned_v2.1.vcf
tabix resources/pruned_v2.1.vcf.gz
```

这将生成一个 `.tbi` 结尾的索引文件。

接着使用 tabix，并指明染色体区域（例：`1:1000-20000`），便可将文件内容提取出来，向 STDOUT 输出。

```zsh
tabix resources/pruned_v2.1.vcf.gz 1:1000-20000 | less -S
```