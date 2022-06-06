grid 是 R 自带的一个绘图基础设施模块，ggplot2 就是基于 grid 开发的。

grid 绘图的逻辑可以大概理解为这几个步骤。

1. 设置一个 viewport，确定绘图的区域（比如左上角四分之一的矩形区域……）
2. 指定 Grob 的位置大小等信息，然后画出这个 Grob（比如一个半径 0.5 的圆）
3. 在当前 viewport 下画别的 Grob，或更换 viewport，在别的地方继续画
4. 如此往复……

## 栗子
以下例子均来自《Mastering Software Development in R》一书。[^1]

用 gTree 将一个圆圈 Grob 和 线段 Grob 组合成一个棒棒糖 gTree。
```r
candy <- circleGrob(r = 0.1, x = 0.5, y = 0.6)
stick <- segmentsGrob(x0 = 0.5, x1 = 0.5, y0 = 0, y1 = 0.5)
lollipop <- gTree(children = gList(candy, stick))
grid.draw(lollipop)
```

典型的 grid 绘图流程：开 viewport，画 Grob，退 viewport。
```r
ex_vp <- viewport(x = 0.5, y = 0.5, 
                  just = c("center", "center"),
                  height = 0.8, width = 0.8,
                  xscale = c(0, 100), yscale = c(0, 10))
pushViewport(ex_vp)
grid.draw(rectGrob())
grid.draw(circleGrob(x = unit(20, "native"), y = unit(5, "native"),
                     r = 0.1, gp = gpar(fill = "lightblue")))
grid.draw(circleGrob(x = unit(85, "native"), y = unit(8, "native"),
                     r = 0.1, gp = gpar(fill = "darkred")))
popViewport()
```

Grob 可以在创建后被修改。[^2]
```r
gl <- linesGrob()
gl <- editGrob(gl, gp = gpar(col = "green"))
```

[^1]: [Mastering Software Development in R](https://bookdown.org/rdpeng/RProgDA/)
[^2]: [Modifying grid grobs](https://stat.ethz.ch/R-manual/R-devel/library/grid/doc/grobs.pdf)