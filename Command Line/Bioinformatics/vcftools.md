VCFtools 是一个用于处理 VCF 文件的命令行软件。

VCFtools 的文档：<https://vcftools.github.io/man_latest.html>

## VCF 格式
VCF 及其他 SAM/BAM 相关文件格式的标准可在 [Samtools 的 Github Pages](https://samtools.github.io/hts-specs/) 上查询。

![[VCF-sample.png]]

VCF 文件本质上就是一个表格，极简的 VCF 只需前 8 列。常见的用于储存不同样本之间 SNP 和 Indel 差异的 VCF 有 9 + N 列，从第 10 列往后，每一列就是一个样本的基因型。

前 9 列内容如下
1. `#CHROM`
2. `POS` 物理位置
3. `ID` SNP 的 ID
4. `REF` 参考基因型
5. `ALT` 变异基因型
6. `QUAL` SNP 质量值
7. `FILTER` SNP 的过滤信息
8. `INFO` SNP 的其他信息
9. `FORMAT` 基因型的格式

Hapmap 与 VCF 的互转可使用 [[TASSEL]] 进行。


## 栗子
### 提取部分个体


### 过滤SNP
通过添加一些参数，VCFtools 可以对读入的 VCF 进行过滤

- `--max-missing`：SNP 的最大缺失比例
- `--maf`：MAF 的最低比例
- `--mac`：MAF 的最低数量
- `--chr`：根据所在的染色体筛选

VCFtools 可根据 SNP 所在位置进行筛选
- `--chr <chromosome>`：包含的染色体
- `--not-chr <chromosome>`：不包含的染色体
- `--from-bp <integer>`：开始的位置
- `--to-bp <integer>`：结束的位置

也可提供一个文本文件。文件内有两列，第一列为染色体，第二列为物理位置
- `--positions <filename>`
- `--exclude-positions <filename>`

### 核苷酸多态性
VCFtools 可进行指定区间的 SNP 的核苷酸多态性 π 值计算。

也可用滑动窗口的方法计算 π 值。
```bash
vcftools \
    --window-pi 200 \
    --window-pi-step 100 \
    --gzvcf my_snp.vcf.gz \
    --keep my_id_list.txt \
    --out my_output_prefix
```

## 其他工具

除了软件本体以外，vcftools 附赠一套 “Perl modules”，用于进行一些特殊的操作。

Perl modules 的文档：<https://vcftools.github.io/perl_module.html>

### vcf-merge

将含有不同个体的 VCF 文件合并在一起。（横向拼接）

```bash
vcf-merge A.vcf.gz B.vcf.gz C.vcf.gz | gzip -c > out.vcf.gz
```

### vcf-concat

将不同染色体的 VCF 合并在一起（纵向拼接）

```bash
vcf-concat A.vcf.gz B.vcf.gz C.vcf.gz | gzip -c > out.vcf.gz
```