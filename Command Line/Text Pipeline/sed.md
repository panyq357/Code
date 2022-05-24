sed 是 Unix 中使用正则表达式处理文本流的程序。

```bash
$ echo "chr1:28427874-28425431" | \
    sed -E 's/^(chr[^:]+):([0-9]+)-([0-9]+)/\1\t\2\t\3/'
chr1 28427874 28425431
```

参数：
- `-e`：用于提供一个写着 sed 脚本的字符串
- `-E`：sed 默认使用 BRE (POSIX Basic Regular Expressions)，改用选项可使其支持 ERE (POSIX Extended Regular Expressions)
- `-n`：不输出无法执行操作的行

注：
> `-E` 在 [sed 的 manual](https://www.gnu.org/software/sed/manual/sed.html) 中的描述如下。
> .... the -E extension has since been added to the POSIX standard, so use -E for portability. GNU sed has accepted -E as an undocumented option for years, and BSD seds have accepted -E for years as well ....

替换命令的末尾字符：
- `g`：全局替换
- `i`：大小写不敏感

## 栗子

替换每一行遇到的第一个 "chrom" 为 "chr"。
```bash
sed -e 's/chrom/chr/' chroms.txt
```

抽取第 20 行到第 50 行之间的所有行。
```bash
sed -n '20,50p' Mus_musculus.GRCm38.75_chr1.gtf
```

将来自 Windows 的文本文件的 CRLF 中的 CR 去掉（也可以用 [[dos2unix]] 完成）。
```bash
sed -e "s/\r//g" file > newfile
```

删掉第 1 行。
```bash
sed -e '1d' my_sequence.fasta
```