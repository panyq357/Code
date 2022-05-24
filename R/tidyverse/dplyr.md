
## 栗子
```r
# 选取表格开头前二十行
top20 <- my_tibble %>% slice_head(n = 20)

# 将表格中的 seqnames 列的名字换成 chr
table_chr <- table_seqnames %>% rename(chr = "seqnames")

# 去除重复的行
my_table_with_no_reps <- my_table %>% distinct(.keep_all = T)
```