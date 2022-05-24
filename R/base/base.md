此处记录了一些 base 中的函数的用法。

## recover
通过以下设置，程序将在运行出错时记录出错的位置，并提供选项，使我们能返回函数调用栈的特定位置，并自动进入 browser() 的 debug 状态。

```r
options(error = recover)
```

## trycatch
trycatch 用于对错误进行处理，用法如下所示。

```r
y <- tryCatch(expr,
    error = function(e){
    message("An error occurred:\n", e)
    },
    warning = function(w){
    message("A warning occured:\n", w)
    },
    finally = {
    message("Finally done!")
    }
)
```

其中 error 和 warning 参数接受的是函数，当 expr 产生错误或警告时，就将其传入对应的函数处理。

如没有错误发生，tryCatch 返回 expr 的值。

finally 则接受一个表达式，无论是否有错误，都会执行表达式里的内容（不能像 error 或 warning 那样写函数，只能是表达式）。

## switch
switch 函数类似于 C 语言中的 switch 语句，其用法如下所示。

```r
y <- switch(x, "A" = 1, "B" = 2, 3)
```

上面这段代码的意思是，如果 x 的值是 "A"，则返回 1，是 "B" 则返回 2，其他则返回 3。

注意：x 必须得是只有一个元素的向量，switch 函数并不支持向量化操作，如需对向量中的所有元素进行操作，可结合 apply 系列函数。

## system2
system2 用于在 shell 中执行命令。相比于更老的 system 函数，它使用起来更方便。

下面这个例子用 tabix 将指定区间的 VCF 内容读进了 R。

```r
chr <- 1
start <- 1000
end <- 2000
vcf_path <- "resources/pruned_v2.1.ann.vcf.gz"

vcf_content <- system2(
    command = "tabix",
    args = c(vcf_path, paste0(chr, ":", start, "-", end)),
    stdout = T
)
```

通过添加 `stdout = TRUE` 参数，system2 函数将返回一个字符型向量，其每个元素就是 STDOUT 中的一行（不包括换行符）。