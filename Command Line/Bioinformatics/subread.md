[subread](http://subread.sourceforge.net) 是一个序列比对软件，同时具有计算 RNA-seq 的 counts matrix 的功能，并且可计算不同转录本之间的差别。

## subread-align
该工具可用于 DNA 或 RNA 的 FASTQ 的比对。

```bash
subread-align -t 0 \
    -T {resources.core_num} \
    -i {input.index_dir}/subread_index \
    -r {input.R1_fastp} \
    -R {input.R2_fastp} \
    -o {output.bam}
```

参数：
- `-t`：实验类型，`0` 是 RNA-seq，`1` 是 DNA
- `-T`：线程数
- `-i`：Index
- `-r`：R1 FASTQ
- `-R`：R2 FASTQ
- `-o`：输出文件名

## featureCounts
该工具适用于 RNA-seq 中 counts matrix 的构建。

```bash
featureCounts -p \
    -T 5 \
    -t exon \
    -g gene_id \
    -a annotation.gtf \
    -o counts.txt \
    mapping_results_SE.sam
```

参数：
- `-p`：双端测序
    - （从 2.0.2 版本以后，这个选项被分成了 `-p` 和 `--countReadPairs` 两个选项。使用户可以决定是用 reads 计数，还是 fragments 计数。）
- `-T`：线程数
- `-t`：feature type
- `-g`：attributes to group feature
- `-a`：GTF 文件路径
- `-o`：输出的 counts 文件路径
