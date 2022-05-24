[bioawk](https://github.com/lh3/bioawk) 为 samtools 和 bwa 的作者 Li Heng 所写的用于处理常见的 fastq、gff、vcf、bed 等格式文件的，扩展自 awk 的程序。

```bash
bioawk -c help
```

参数：
- `-c`：用于指定处理文件的格式
    - `fastx`：自动识别 FASTQ 和 FASTA
    - `hdr`：自动识别第一行为表头的文本表格文件，并将表头名作为 Field 变量名

## 栗子
统计 FASTQ 条数。
```bash
bioawk -c fastx 'END{print NR}' contam.fastq
```

FASTQ 转 FASTA。
```bash
bioawk -c fastx '{print ">"$name"\n"revcomp($seq)}' contam.fastq
```

统计每条 FASTA 的长度。
```bash
bioawk -c fastx '{print $name,length($seq)}' \
    Mus_musculus.GRCm38.75.dna_rm.toplevel.fa.gz
```

处理普通的表格文件。
```bash
$ head -n genotypes.txt
id ind_A ind_B ind_C ind_D
S_000 T/T A/T A/T T/T
S_001 G/C C/C C/C C/G
S_002 C/A A/C C/C C/C
$ bioawk -c hdr '$ind_B == $ind_C {print $id}' genotypes.txt
S_000
S_001
```