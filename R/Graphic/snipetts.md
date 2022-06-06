
Y 轴下限不延伸，上限延伸 0.2
```R
scale_y_continuous(expand = expansion(mult = c(0, 0.2)))
```

X 轴标签倾斜 45 度
```R
theme(axis.text.x = element_text(angle = 45,hjust = 1))
```

bar、errorbar、jitter 三件套（注：其中用到的 mean_sdl 函数需要安装 Hmisc 包）
```R
	geom_bar(stat = "summary",
             fun = "mean",
             na.rm = T,
             width = .7,
             color = "black",
             alpha = 0) +
    geom_errorbar(stat = "summary",
                  fun.data = mean_sdl,
                  fun.args = list("mult" = 1),
                  na.rm = T,
                  width = .6) +
    geom_jitter(height = 0,
                alpha = .5,
                na.rm = T)
```

绘制饼图
```R
pie <- ggplot(chr4_29662946) +
    geom_bar(aes(x = "Allele", fill = Allele)) +
    coord_polar(theta="y")
```

将横向分面之间的空隙设为 0 

```r
theme(panel.spacing.x = unit(0,"line"))
```