rsync 是一个用于在不同的主机间同步文件的命令行工具，即 **r**emote **sync**。

```bash
rsync -Pavz [directory] [user]@[server]:[distination]
```

## 参数
- `-P`：显示传输进程，并允许中断后恢复传输
- `-a`：传输文件时也顺带传输文件的各种属性
- `-v`：输出传输细节
- `-z`：在传输过程中压缩文件
- `-r`：递归传输目录内的所有子目录和文件

## 参考
-   [StackExchange 中的回答](https://unix.stackexchange.com/a/39248)
-   [阮一峰的 rsync 教程](https://www.ruanyifeng.com/blog/2020/08/rsync.html)