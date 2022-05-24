
## 栗子

```bash
fastp \
    --thread {resources.core_num}
    --in1 {input.R1} \
    --in2 {input.R2} \
    --out1 {output.R1} \
    --out2 {output.R2} \
    --html {output.html} \
    --json {output.json} \
    --report_title {wildcards.antigen}_{wildcards.sample}_{wildcards.rep}_{wildcards.input_ip}
```

其中 
- `--html` 指定输出的 html 报告的路径
- `--json` 指定输出的 json 文件的路径
- `--report_title` 指定 html 报告的标题

## 资源占用

- 内存：不超过 1 G（无选项可指定内存）
- 线程数：4 个线程就够了

> 参考：[fastp memory usage and speed up](https://github.com/OpenGene/fastp/issues/83)

