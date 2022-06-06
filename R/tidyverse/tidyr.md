
## separate 函数：分割一列
[在线文档](https://tidyr.tidyverse.org/reference/separate.html)

```r
separate(
  data,
  col, # 要分裂的列
  into, # 分裂后新生成的列的列名，新生成的列会替代原来的列的位置
  sep = "[^[:alnum:]]+", # 分裂的分隔符
  remove = TRUE,
  convert = FALSE,
  extra = "warn",
  fill = "warn",
  ...
)
```