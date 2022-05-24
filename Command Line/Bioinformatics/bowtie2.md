在线文档：<http://bowtie-bio.sourceforge.net/manual.shtml>
													   
### 建索引

bowtie2 的建索引命令 `bowtie2-build` 并不支持 gzip 压缩的 `.fastq.gz` 文件，所以需要先解压再建索引。

```bash
zcat < {input.ref_fa_gz} > {output.ref_fa}
bowtie2-build {output.ref_fa} {params.prefix}
```

根据[文档](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#the-bowtie2-build-indexer)，`bowtie2-build` 将生成以下六个文件

> `bowtie2-build` outputs a set of 6 files with suffixes `.1.bt2`, `.2.bt2`, `.3.bt2`, `.4.bt2`, `.rev.1.bt2`, and `.rev.2.bt2`.

### 比对

```bash
bowtie2 \
    -q \
    --local \
    --threads {resources.core_num} \
    -x {params.index} \
    -1 {input.R1} \
    -2 {input.R2} \
	> {output}
```

其中
- `-q` 指定读入的文件为 FASTQ 格式（支持 `.fastq` 和 `.fastq.gz`）
- `--local` 指定比对模式为 `local`（详情见[文档](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#local-alignment-example)）
- `--threads` 指定线程数
- `-x` 指定索引文件的前缀
- `-1` 和 `-2` 指定读入的 `.fastq.gz` 文件

### 管道

```bash
bowtie2 \
    -q --local \
    --threads {resources.core_num} \
    -x {params.index} \
    -1 {input.R1} \
    -2 {input.R2} | \
samtools view \
    -b -S -h \
    > {output.bam}
```