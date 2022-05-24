uniq 是 Unix 中用于给文件去除重复的行的命令。

```bash
uniq -c letters.txt
```

选项：
- `-c`：在输出的开头添加一列，写着每一行出现了多少次。
- `-d`：只输出有重复的行。