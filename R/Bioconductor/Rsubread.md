[subread](http://subread.sourceforge.net) 是一个像 bowtie2、bwa 一样的序列比对软件，[Rsubread](http://bioconductor.org/packages/release/bioc/html/Rsubread.html) 是 subread 的一个 R 语言包装版。

## 栗子
用 Rsubread 进行序列比对也需要先建索引。
```r
library(Rsubread)
dir.create("resources/index", recursive=T)
buildindex(basename = "resources/index/os_index", reference = "rawdata/IRGSP-1.0_genome.fasta.gz")
```

用 `Rsubread::align` 函数进行双端测序比对的示例如下。
```r
library(Rsubread)
samples <- c("sample1", "sample2", "sample3")
dir.create("resources/rsubread")
for (sample in samples) {
    align(index="resources/index/os_index",
          readfile1=sprintf("resources/fastp/%s.R1.fastq.gz", sample),
          readfile2=sprintf("resources/fastp/%s.R2.fastq.gz", sample),
          input_format="gzFASTQ",
          output_file=sprintf("resources/rsubread/%s.bam", sample),
          nthreads=16)
}
```

用 `Rsubread::featureCount` 函数获得 RNA-seq counts 矩阵并传递给 edgeR 进行下一步分析。
```r
library(Rsubread)
library(edgeR)

# Use Rsubread featureCounts to generate counts matrix
bams <- list.files("resources/rsubread", pattern="*.bam$", full.name=T)
fc <- featureCounts(
    files=bams,
    annot.ext="rawdata/IRGSP-1.0_representative_transcript_exon_2022-03-11.gtf",
    isGTFAnnotationFile=TRUE,
    GTF.featureType="exon",
    GTF.attrType="gene_id",
    isPairedEnd=TRUE
)

# Pass counts matrix to edgeR
colnames(fc$counts) <- gsub(".bam", "", colnames(fc$counts))
group <- factor(substr(colnames(fc$counts), 1, 2))
y <- DGEList(fc$counts, group=group)
y$genes <- fc$annotation[, "Length", drop=FALSE]

```