# AnnotationHub

```r
ah <- AnnotationHub()
display(ah)
```

通过键入以上代码可打开一个 shiny 网页，从而快速查找到需要的数据的信息。

### 数据集操作

```R
# 获取来自 NCBI 的粳稻注释数据集
osj <- ah[["AH96212"]]

# 查看该数据集有哪些信息可供查询
columns(osj)

# 查看用于调取数据的的 key（通常是基因 ID）
keys(osj)

```
