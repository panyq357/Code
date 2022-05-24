showtext 是一个使 R 语言可以使用自定义字体进行画图的包。

```R
install.packages("showtext")
library(showtext)
```

全局启用 showtext
```R
# 全局启用 showtext
showtext_auto()
# 关闭全局 showtext
showtext_auto(FALSE)
```

在指定代码块范围内使用 showtext
```R
showtext_begin()
# some codes...
showtext_end()
```

showtext 可调用 sysfonts 包来载入系统内的字体文件
```R
# 列出字体文件及其路径
font_files()

# 列出用于搜索字体文件的目录路径
font_paths()

# 添加一个搜索路径
font_paths("~/my_fonts")

# 使得 ggplot 和 base plot 可以用 family="Arial" 参数，
# 来调用 "Arial Unicode.ttf" 的字体
font_add("Arial", "Arial Unicode.ttf")

```

一个栗子
```R
library(showtext)
library(ggplot2)

font_add("Arial", "Arial Unicode.ttf")
font_add("Times", "Times New Roman.ttf")

showtext_auto()

pdf("compare.pdf")
ggplot() +
    geom_text(aes(x=0, y=1, label="Hello, World!"), family="Arial") +
    geom_text(aes(x=0, y=2, label="Hello, World!"), family="Times") +
    xlim(-1, 1) +
    ylim(0, 3)
dev.off()
```

