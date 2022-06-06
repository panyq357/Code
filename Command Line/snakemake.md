## 栗子



### One input, multiple output with multiple params.

```snakemake
CELL_TYPE = ["rice", "yeast", "human"]

rule all:
	input:
		expand("results/my_output_{cell_type}", cell_type = CELL_TYPE)

rule my_rule:
	input:
		"raw_data/my_data.csv"
	params:
		type_of_cell = "{cell_type}"
	log:
		"logs/my_log_{cell_type}"
	output:
		"results/my_output_{cell_type}"
	script:
		"scripts/my_script.R"
```

## [snakemake: How to log python scripts executed by script directive?](https://stackoverflow.com/questions/64101921/snakemake-how-to-log-python-scripts-executed-by-script-directive)

To redirect error messages, you need to use ``type`` argument.

```
log <- file(snakemake@log[[1]], open="wt")
sink(log, type = c("output", "message"), split = F)
[rest of script]
```

## Using Snakemake in Cluster

```bash
bsub snakemake --cluster 'bsub -R "rusage[mem={resources.mem_mb}]"' --jobs 26 --default-resources
```

Refs
1. <https://snakemake.readthedocs.io/en/stable/executing/cluster.html>
2. <https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=o-r>