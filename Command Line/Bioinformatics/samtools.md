[samtools Manual](http://www.htslib.org/doc/samtools.html)

### samtools view
功能：查看和过滤。输入可以是 SAM 或 BAM 格式（自动识别），输出默认为 SAM 格式。[在线文档](http://www.htslib.org/doc/samtools-view.html)

染色体区域参数写法可以是 `chr1`、`chr2:10000`（从 10000 到结束）或`chr3:2000-3000`。

```bash
samtools view my_alignment.bam chr1:10000-20000
```

- `-b`：设置输出格式为 BAM
- `-o`：设置输出文件路径
- `-h`：在输出中保存头部信息

### samtools sort

功能：排序。输入可以是 SAM 或 BAM 格式（自动识别），输出默认为 BAM 格式（默认 STDOUT）。[在线文档](http://www.htslib.org/doc/samtools-sort.html)

```bash
samtools sort my_alignment.bam
```

- `-o`：设置输出文件路径
- `-O`：设置输出格式，可以是 `sam`、`bam` 或 `cram`，如果设置了 `-o` 选项，可根据扩展名自动识别


### samtools flagstat

获取一个 BAM 文件的比对质量相关的统计信息，输出到 STDOUT

```bash
samtools flagstat test.bam
```

### samtools fasta / fastq

将 SAM 或 BAM 转成 FASTA 或 FASTQ。

```
samtools fasta in.bam > out.fasta
samtools fastp in.bam > out.fastp
```