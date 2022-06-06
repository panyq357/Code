---
title: VennDiagram
tags:
    - R
    - CRAN
    - Visualization
---

VennDiagram 是一个绘制韦恩图的 R 包，它基于 grid 包。[^1][^2]

## 栗子
venn.diagram 函数是主要的作图函数。

```r
venn.diagram(
    x = list(set1, set2, set3),
    category.names = c("Set 1" , "Set 2 " , "Set 3"),
)
```

[^1]: [R语言：VennDiagram绘制venn图](https://www.jianshu.com/p/f858521828a5)
[^2]: [Venn Diagram – the R Graph Gallery](https://r-graph-gallery.com/14-venn-diagramm.html)