[radian](https://github.com/randy3k/radian) 是一个用 python 写的增强版 R console。

radian 的配置文件位于 `~/.radian_profile`，可通过在其中添加选项修改 radian 的设置。常用设置如下所示。

```R
# No space in bottom and disable suggestion window.
options(radian.complete_while_typing = FALSE)

# Disable auto quotes and parens matching.
options(radian.auto_match = FALSE)
```