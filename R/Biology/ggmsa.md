---
title: ggmsa
author: panyq
tags:
    - R
    - Bioconductor
    - MSA
---
ggmsa 是余光创所作的用于绘制 MSA 序列比对图的 R 包。

- [ggmsa 的主页](http://yulab-smu.top/ggmsa/articles/ggmsa.html)
- [ggmsa 的 bioconductor 页面](http://bioconductor.org/packages/release/bioc/html/ggmsa.html)




```r
ggmsa("ortholog-sequences-protein.fa",  # MSA 文件路径（FASTA 等格式）
      start = 224 - 20,
      end = 224 + 20,
      font = "mono",
      char_width = 0.5,
      seq_name = TRUE) +
    geom_seqlogo(color = "Chemistry_AA") +  # 在上方显示 seqlogo 统计
    geom_msaBar()  # 在下方显示 consensus 柱状图
```