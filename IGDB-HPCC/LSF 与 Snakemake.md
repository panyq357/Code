[Snakemake](https://snakemake.readthedocs.io/en/stable/) 是一个流行的流程管理软件，它可以将不同的分析步骤串在一起，提高执行的效率和可重复性。

## Snakemake 与集群
snakemake 提供了与高性能计算集群进行协作的功能，详情可见文档[^1]。以下是一个典型的 Snakemake 与 LSF 联用的例子。

```bash
snakemake \
	--cluster 'bsub -n {resources.core_num} -R "rusage[mem={resources.mem_gb}]" -o {log}' \
	--default-resources core_num=1 mem_gb=1 \
	--jobs 24
```

其中：
- `--cluter`：指定提交任务的命令及其参数，其中可使用 Snakemake 的 `{}` 语法嵌入变量
- `--default-resources`：后跟空格分隔的键值对，指定每个任务所需的的默认资源
- `--jobs`：指定最大的提交任务的数量

在 Snakefile 所在目录执行这段命令，便可将向作业管理系统批量地提交作业。

## 参考
[^1]: [Snakemake - Cluster Execution](https://snakemake.readthedocs.io/en/stable/executing/cluster.html)