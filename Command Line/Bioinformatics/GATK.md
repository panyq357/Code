很多原本属于 Picard 的工具都被归进了 GATK4 中。

有关各个工具该用多少核心，多少内存，可参考《A practical introduction to GATK 4 on Biowulf (NIH HPC)》[^4]

## MarkDuplicates
该工具用于标记/去除重复的序列。需要 BAM 文件是排好序的。[在线文档](https://gatk.broadinstitute.org/hc/en-us/articles/360037052812)

尽管文档里没提，但该工具还需要每条序列的 @RG 中有 ID 和 SM 两个 tag。

还有，MarkDuplicates 并不能从 STDIN 中读取输入。[^2]

```bash
gatk --java-options "-Xmx12G" MarkDuplicates \
    --REMOVE_DUPLICATES true \
    --INPUT input.bam \
    --OUTPUT output.bam \
    --METRICS_FILE dup_metrics.txt \
    --CREATE_INDEX true
```

在设置了 `--CREATE_INDEX true` 后，将会生成一个与输出的 bam 相同前缀的 .bai 索引文件，例如上面的例子会生成 `output.bai` 文件。

## HaplotypeCaller

虽然叫 HaplotypeCaller，但文档说它也适用于混池测序的 SNP calling。[^3][在线文档](https://gatk.broadinstitute.org/hc/en-us/articles/360036897532)

HaplotypeCaller 需要参考基因组 FASTA 文件有两个索引。[^5]可用以下命令生成。

```bash
samtools faidx ref.fasta
gatk CreateSequenceDictionary -R ref.fasta
```

这将生成两个文件 `ref.fasta.fai` 和 `ref.dict`。

```bash
gatk --java-options "-Xmx{resources.mem_gb}G" HaplotypeCaller \
    -R {input.ref_genome_fa} \
    -I {input.filtered_bam} \
    -ERC GVCF \
    -O {output.g_vcf_gz}
```




[^1]: [Picard FAQ](http://broadinstitute.github.io/picard/faq.html)
[^2]: [Piping Markduplicates](https://www.biostars.org/p/83286/)
[^3]: [HaplotypeCaller](https://gatk.broadinstitute.org/hc/en-us/articles/360036897532)
[^4]: [A practical introduction to GATK 4 on Biowulf (NIH HPC)](https://hpc.nih.gov/training/gatk_tutorial/)
[^5]: [FASTA - Reference genome format](https://gatk.broadinstitute.org/hc/en-us/articles/360035531652)