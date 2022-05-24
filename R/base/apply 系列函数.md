虽然相比于 [[purrr]] 包中的 map 系列函数，base R 的 apply 系列函数命名和使用方法都更不规整，但其功能同样强大，也更贴合 base R 的“氛围”。

parallel 包中则提供了多线程版的以 "mc"(multi-core) 开头的 apply 系列函数，使用方法大同小异。

```
mapply(FUN, ..., MoreArgs = NULL, SIMPLIFY = TRUE, USE.NAMES = TRUE)
```

