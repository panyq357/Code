pigz 是一个多线程的压缩软件，支持 gzip 等多种格式。

pigz 的 Github 仓库：<https://github.com/madler/pigz>

## 栗子
用 10 个线程进行压缩（默认会删除原文件）
```bash
pigz -p 10 my_file.txt
```

解压
```bash
pigz -dc my_file.txt.gz > my_file.txt
```
