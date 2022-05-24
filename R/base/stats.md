## aggregate
aggregate 函数的功能类似于 dplyr 包中的 group_by 函数，以及 [doBy](https://cran.r-project.org/web/packages/doBy/index.html) 包中的 summaryBy 函数，即分组计算。

```r
aggregate(x = iris[c("Sepal.Length","Sepal.Width")],
          by = list(group = iris$Species),
          FUN = mean)
```

上述代码输出如下。

```r
       group Sepal.Length Sepal.Width
1     setosa        5.006       3.428
2 versicolor        5.936       2.770
3  virginica        6.588       2.974
```