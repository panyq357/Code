[SnpEff](http://pcingola.github.io/SnpEff/se_introduction/) 是一个对 VCF 和 BED 文件中的 SNP 进行注释的软件。

SnpEff 可以自动识别 gzip 压缩的 VCF，并且可通过设置文件名为 `-` 从 STDIN 读取 VCF。

SnpEff 的数据库中已经有许多物种的注释数据（比如水稻是 `Oryza_sativa`）。

- `-t`：多线程
- `-ud`：控制上下游范围
- `-s`：输出的 summary html 的路径

经 SnpEff 注释的 VCF，在 INFO 列会新增以 `ANN` 开头的注释，并在文件头部添加一些注释行。[^1]

SnpEff 默认需要 8G 内存，这足以分析人类的 vcf 文件。[^2]

## Build Database
### GTF
首先，写一个 `snpEff.config` 文件。
```
# DIY genome, version DIYgenome1.0
DIYgenome1.0.genome : DIYspecies
```

然后修改基因组 FASTA 文件和 GTF 注释文件的文件名，放到同一目录下。

最后，用 snpEff build databas。
```bash
snpEff build -gtf22 -v DIYgenome1.0
```

## 栗子

列出 SnpEff 中已经有的数据库

```zsh
snpeff databases | less -S
```

列出数据库，以 html 格式呈现

```zsh
snpeff databases html > ~/Desktop/snpeff.html
```

用水稻的注释数据库注释 VCF 文件

```zsh
snpeff -v Oryza_sativa resources/pruned_v2.1.vcf.gz | bgzip -c > resources/pruned_v2.1.ann.vcf.gz
```


[^1]: [注释的格式的文档](http://pcingola.github.io/SnpEff/se_inputoutput/#ann-field-vcf-output-files)
[^2]: [SnpEff FAQ](https://pcingola.github.io/SnpEff/se_faq/)