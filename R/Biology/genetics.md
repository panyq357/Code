genetics 包中包含一些基础的统计遗传学相关函数

## 栗子
genotype 函数可对一个基因型字符串进行解析，进行一些简单的统计。
```R
> x <- c("AA", "AT", "TT", "TT")
> gx <- genotype(x, sep="", reorder="freq")
> gx
[1] "A/A" "T/A" "T/T" "T/T"
Alleles: T A
> allele.names(gx)
[1] "T" "A"
```

