TASSEL 本是用于进行 GWAS 的软件，但也包含了很多其他的功能，比如格式转换等。

## 栗子
### Sort Hapmap 文件
要对 Hapmap 文件中的 SNP 按染色体和物理位置进行排序，可使用 TASSEL 自带的插件完成。

```bash
run_pipeline.pl \
    -Xmx10g \
    -SortGenotypeFilePlugin \
    -inputFile input.hmp.txt \
    -outputFile output.sort \
    -fileType Hapmap \
    -endPlugin
```

这将生成一个 output.sort.hmp.txt 文件。

### 格式转换
TASSEL 可进行一些简单的格式转换。

注意：需要确保 Hapmap 文件是排过序的

```bash
run_pipeline.pl \
    -Xmx10g \
    -fork1 \
	    -h input_path \
	    -export output_prefix \
	    -exportType Plink \
	-runfork1
```

输入文件格式可通过不同的参数控制。

- `-h <hapmap file>`：读入 Hapmap 文件
- `-vcf <filename>`：读入 VCF 文件
- `-plink -ped <ped filename> -map <map filename>`：读入 PLINK 的 ped 和 map 文件

输出文件格式由 `-exportType <type>` 控制。

- `Plink`
- `Hapmap`
- `VCF`

转换成不同的格式，生成的文件后缀名不一样。

- `Plink`：`{prefix}.plk.ped` 和 `{prefix}.plk.map`
- `VCF`：`{prefix}.vcf`

## 参考
- [Tassel 5.0 Pipeline Document](https://bytebucket.org/tasseladmin/tassel-5-source/wiki/docs/Tassel5PipelineCLI.pdf "Tassel 5.0 Pipeline Document")