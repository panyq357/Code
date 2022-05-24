[argparse](https://docs.python.org/3/library/argparse.html)是标准库中用于解析命令行参数的模块。

基本用法如下（这是一个改正并合并 hapmap 文件的脚本）

```python
import argparse

parser = argparse.ArgumentParser(description='Adjust and concate hmp files.')

parser.add_argument('-i', type=str, dest="in_path", nargs="*", help='path to input files')
parser.add_argument('-o', type=str, dest="out_path", help='path to output file')

args = parser.parse_args()

out_file = open(args.out_path, "w")

# Copy header only once
with open(args.in_path[0], "r") as in_file:
    header = in_file.readline().strip().split("\t")
    out_file.write("\t".join(header) + "\n")


# Read and write, line by line
for in_path in args.in_path:
    with open(in_path, "r") as in_file:
        another_header = in_file.readline().strip().split("\t")
        if another_header != header:
            raise Warning("Different header found in: " + in_path)
        for line in in_file:
            line = line.strip().split("\t")
            line[2] = str(int(line[0][-2:]))
            line[0] = line[2] + "-" + line[3]
            out_file.write("\t".join(line) + "\n")

out_file.close()


```