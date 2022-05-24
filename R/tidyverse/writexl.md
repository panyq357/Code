writexl 包用于将表格写入 Excel 的 .xlsx 文件中。

## 栗子
```r
# 写入 .xlsx 文件
# 这里的 x 可以是一个表格，也可以是一个由表格组成的列表。
# 如果是一个由表格组成的列表，则写进不同的 sheet 中。
writexl::write_xlsx(x, "snp_table_subset.xlsx")
```