## reduce
就像斐波那契数列的两两相加一样，reduce 函数可将一个 list 内的元素进行两两处理。

例如下面这个例子，就将一个 list 内的所有 tibble 都 full_join 了起来。[^1]
```r
list(x, y, z) %>% reduce(left_join, by = "i")
```



[^1]: [Simultaneously merge multiple data.frames in a list](https://stackoverflow.com/questions/8091303/simultaneously-merge-multiple-data-frames-in-a-list)