---
tags:
    - CommandLine
    - Image
---

rsvg-convert 是一个用来将 svg 图片转换成别的格式的命令行工具。

## 栗子

以下内容来自涛叔[^1]

`rsvg-convert` 的用法非常简单，只需要一个`-h` 参数指定输出的 png 高度即可：

```
for icon in $(ls icons/|grep svg); do
  for size in 32 64 128; do
    rsvg-convert -h $size icons/$icon > icons/${icon%.svg}-$size.png
  done
done
```

[^1]: [SVG 转 PNG 图片](https://taoshu.in/svg-to-png.html)