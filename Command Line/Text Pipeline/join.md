join 是 Unix 中用于 merge 不同的文本表格文件的程序。

注意⚠️：用于 join 的文件必须先 sort！

```bash
join -1 1 -2 1 example_sorted.bed example_lengths.txt > example_with_lengths.txt
```

选项：
- `-1`：第一个文件中当作键的列
- `-2`：第二个文件中当作键的列
- `-a`：用于指定，那个文件中的没有和另一个文件匹配上的行可以被保留下来（GNU/Linux 限定）