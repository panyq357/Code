grep 是 Unix 下一个用正则表达式抽取文本文件中指定行的程序。

## 栗子
1、检查文件是否具有非 ASCII 字符（GNU/Linux 限定）。其原理就是看字符在不在 ASCII 字符的区间内。
```bash
LC_CTYPE=C grep --color='auto' -P "[\x80-\xFF]" improper.fa
```