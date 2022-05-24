[PLINK](https://www.cog-genomics.org/plink/1.9/) 是一个对 SNP 数据进行过滤和分析的软件，最后的版本是 1.90。

[PLINK2](http://www.cog-genomics.org/plink/2.0/) 是 PLINK 的延续开发，具有更多的功能和更好的性能，但对一些参数的名称和用法作出了修改。

## 栗子
### bed 格式转 vcf
```bash
# PLINK 版
plink \
    --bfile bfile_prefix \
    --recode vcf-iid bgz \
    --out vcf_prefix
# PLINK2 版
plink2 \
    --bfile bfile_prefix \
    --export vcf bgz id-paste=iid \
    --out vcf_prefix
```

注意⚠️：其中的 `vcf-iid` 和 `id-paste=iid`。由于 bed 格式中有 FID 和 IID 两个 ID，如果不加这些参数，仅输出 vcf 的话，PLINK/PLINK2 就会把 FID 和 IID 用下划线连起来，作为 ID 输出。

在 `--recode` 和 `--export` 后面添加 `bgz` 可使输出自动用 bgzip 压缩，方便之后用 tabix 建索引提取区间。

### 输入控制

PLINK 可按一定规则对输入数据进行筛选。[相关文档](https://www.cog-genomics.org/plink/1.9/filter)

```bash
# 按染色体进行筛选
--chr <number(s)/range(s)...>
--not-chr <number(s)/range(s)...>

# 按染色体上的物理位置进行筛选
--from-bp <pos>  
--to-bp <pos>  
--from-kb <kb pos>  
--to-kb <kb pos>  
--from-mb <mb pos>  
--to-mb <mb pos>
```

### 输出控制

