[aria2](https://aria2.github.io) 是一个可在在 Linux 命令行中进行高速批量下载的软件，`aria2c` 是它的二进制文件。

## 参数

- `-i, --input-file=<FILE>`：下载文件中列出的下载链接
- `-c, --continue[=true|false]`：断点续传

## 使用示例

下载单个文件。
```bash
aria2c http://example.com/example_file.txt
```

下载多个文件，中断后再执行可断点续传。
```bash
arai2c --continue=true --input-file=my_urls.txt
```