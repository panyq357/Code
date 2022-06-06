## capture.outputs
将命令的输出一行一行地作为字符串向量存起来。
```r
HARV_dsmCrop_info <- capture.output(
  GDALinfo("data/NEON-DS-Airborne-Remote-Sensing/HARV/DSM/HARV_dsmCrop.tif")
)
```
