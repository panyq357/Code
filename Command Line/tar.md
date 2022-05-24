
## 栗子
```bash
tar -xzO \
    -f rawdata/IRGSP-1.0_representative_2022-03-11.tar.gz \
    > resources/locus.gff
```

参数：
- `-x`：解压模式
- `-c`：压缩模式
- `-t`：列出压缩包内容
- `-z`：压缩格式为 gzip
- `-f`：设定压缩包路径
- `-O`：向 STDOUT 解压
- `-C`：向指定目录解压
