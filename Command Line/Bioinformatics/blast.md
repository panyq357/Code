
[BLAST® Command Line Applications User Manual](https://www.ncbi.nlm.nih.gov/books/NBK279690/)

## 栗子
makeblastdb：创建本地的 BLAST 数据库

```bash
makeblastdb \
    -in resources/os_genome.fasta \
    -input_type fasta \
    -dbtype nucl \
    -title os \
    -out resources/os_blastn_db
```

blastn：进行 BLASTn 搜索

```bash
blastn \
    -db resources/os_blastn_db \
    -query resources/xr1/xr1_sorted_mapped.fa \
    -out resources/xr1/xr1_sorted_mapped_blasted.tsv \
    -perc_identity 100 \
    -max_target_seqs 1 \
    -evalue 1e-05 \
    -outfmt "6 std qlen" \
    -num_threads 20
```


