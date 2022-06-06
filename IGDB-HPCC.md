---
title: IGDB-HPCC
author: panyq
tags:
    - Linux
    - Cluster
---

IGDB-HPCC 集群用的作业管理系统为 IBM 的 LSF。

IBM 的 LSF 是支持 Spark 的。[^4]

## LSF

### bsub
提交任务。
```bash
bsub -n 1 -q vvl -o job.out ./myprog "-input data.txt"
```

- `-q`：指定队列
- `-n`：指定所需核心数
- `-R`：指定所需资源
	- `-R "select[hname=b001]"`：指定运行节点为 b001
	- `-R "rusage[mem=10]"`：指定内存用量为 10G
- `-o`：指定日志路径

bsub 还可用来启动一个可交互的 shell [^1][^2][^3]。（IGDB-HPCC 的 vvl 队列不支持启动交互式 shell，其他队列支持）
```bash
bsub -q low -Is bash
```

用 `-R` 参数指定内存和磁盘用量时，只给了一个数字（比如 `-R "rusage[mem=10]"` 中的 `10`），数字的单位可通过查询 LSF 的配置文件得知。
```bash
cat ${LSF_ENVDIR}/lsf.conf | grep LSF_UNIT_FOR_LIMITS
```

### bjobs
查询正在运行的任务信息。
```bash
bjobs -l $MY_JOBID
```

- `-l`：显示详细信息
- `-p`：显示处于 pending 状态的任务
- `-s`：显示处于 suspending 状态的任务

如果不加任务 ID，则列出所有正在运行的任务。

### bhist
查询任务历史。
```bash
bhist -l $MY_JOBID
```

- `-l`：显示详细信息

### bkill
提前结束任务。
```bash
bkill -r $MY_JOBID
```

- `-r`：不等待操作系统的结束信号，强制终止

### 其他命令
- `bhosts`：查询集群节点列表
- `bqueues`：查询队列信息
- `lsload`：查询节点负载

## 参考
[^1]: [HBS manual about interactive jobs](https://grid.rcs.hbs.org/starting-interactive-jobs)
[^2]: [Platform™ manual about Interactive jobs](http://sunray2.mit.edu/kits/platform-lsf/7.0.6/1/guides/kit_lsf_guide_source/admin/interactivebsub.html)
[^3]: [LSF Interactive jobs document](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=tasks-interactive-jobs-bsub)
[^4]: [About LSF with Apache Spark](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=spark-about-lsf-apache)
[^5]: [Batch System Primer](https://hpc.llnl.gov/banks-jobs/running-jobs/batch-system-primer)