文档：<https://lomereiter.github.io/sambamba/docs/sambamba-view.html>

sambamba 的默认输入为 BAM 格式。
sambamba 默认不从 STDIN 读取数据，如要将命令写进管道，可将输入文件路径替换为 `/dev/stdin`。
sambamba 会自动生成 `.bai` 索引文件。

> ⚠️：不同的子命令的输入输出行为不尽相同
> ⚠️：尽量不要将命令写入管道，可能引发未知的问题，且等待排错的时间较长

### 基本用法

#### sam 转 bam

`sambamba view` 的默认输入时 BAM 文件，默认向 STDOUT 输出 SAM 格式。
在转换 SAM 为 BAM 时，需指定 `--sam-input` 和 `--format=bam` 参数

```bash
sambamba view \
    --nthreads {resources.core_num} \
    --with-header \
    --sam-input \
	--format=bam \
    {input} > {output}
```

> ⚠️：根据[文档](https://lomereiter.github.io/sambamba/docs/sambamba-view.html#OPTIONS)：`--format=sam` 中的 `sam` 要小写

#### Sort

> ⚠️：`sambamba sort` 默认不往 STDOUT 输出而是生成一个 `.sorted.bam` 文件。如需将其并入管道，需指定 `--out` 参数为 `/dev/stdout`。

```bash
sambamba sort \
    --nthreads {resources.core_num} \
    --memory-limit {resources.mem_gb}G \
	--out {output} \
    {input}
```

#### MARkdup

根据[文档](https://lomereiter.github.io/sambamba/docs/sambamba-markdup.html)描述，sambamba 的 `markdup` 的标准与 Picard 相同，内存使用大概为每 100M reads 占用 2G 内存（没有指定内存的选项）。

> ⚠️：`sambamba markdup` 的输出参数与其他命令不太一致

```bash
sambamba markdup \
    --nthreads {resources.core_num} \
    {input} {output}
```

