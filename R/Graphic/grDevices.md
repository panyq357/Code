
在 MacOS 下用命令行中的 R 进行绘图时，键入绘图函数后，会弹出一个窗口展示画出的图。[grDevices](https://www.rdocumentation.org/packages/grDevices/versions/3.6.2) 就是 R 语言中负责弹出绘图窗口的包。

通过 grDevices 包中的一些函数可以修改这个窗口的样式。比如在 MacOS 中，默认设置可由 `quartz.options` 函数修改。

```R
grDevices::quartz.options(
	width = 8,
	height = 6,
	pointsize = 10,
	reset = FALSE
)
```