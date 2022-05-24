[GEMMA](https://github.com/genetics-statistics/GEMMA) 是一个高效的 GWAS 软件。

## 基本用法
### 0. 输入数据

基因型数据用 PLINK 的 BED 三件套即可。

表型文件数据可直接替换进 FAM 文件的第六列（注意顺序要对好）。

### 1. 构建亲缘矩阵
```bash
gemma -bfile [prefix] -gk [num] -o [prefix]
```

- `-bfile`：PLINK 的 BED 格式的文件的前缀
- `-gk`：可以是 1 或者 2，代表使用不同的算法
    - `1`：centered relatedness matrix，当低 MAF 的 SNP 的 Effect size 有更大的影响时，考虑用此算法
    - `2`：standardized relatedness matrix，当 MAF 对 SNP 的 Effect size 没影响时，用此算法即可
- `-o`：输出的亲缘矩阵文件的前缀

### 2. 关联分析
```bash
gemma -bfile [prefix] -k [filename] -lmm [num] -o [prefix]
```

- `-bfile`：PLINK 的 BED 格式的文件的前缀
- `-k`：亲缘矩阵文件路径
- `-lmm`：不同的检测方法
    - `1`: Wald test
    - `2`:  likelihood ratio test
    - `3`:  score test
    - `4`:  all the three tests