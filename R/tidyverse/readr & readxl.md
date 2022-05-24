### `col_types` 在 `readr` 和 `readxl` 中是不同的

在 `readr` 和 `readxl` 包中的许多读取表格的函数中都有 `col_types` 参数，但这两个包中的这个同名参数的用法却不一样。

在 `readr` 中 `col_types` 参数接收 `cols` 或 `cols_only` 对象，具体用法参考 [readr 的文档](https://readr.tidyverse.org/reference/cols.html)。

```R
# 所有列的数据类型都设为字符型
my_csv <- readr::read_csv("my_data.csv", col_types = cols(.default = col_character()))
```

而在 `readxl` 中，`col_types` 参数则接收一个字符串向量，具体用法参考 [readxl 的文档](https://readxl.tidyverse.org/articles/cell-and-column-types.html?q=col_types#excel-types-r-types-col_types)。

```R
# 所有列的数据类型都设为字符型
my_excel <- readxl::read_excel("my_excel.xlsx", col_types = "text")
