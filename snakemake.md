
若要 debug snakemake pipeline 中的 R 脚本，可在 R 脚本中加入 save.image 函数，然后运行 snakemake，等 snakemake 运行结束后，再手动重启 R，恢复保存的环境，进行 debug。