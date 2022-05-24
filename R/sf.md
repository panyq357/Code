---
title: "Simple Features for R"
---

[sf](https://r-spatial.github.io/sf/index.html) 包是一个用于读取和操作一些地理绘图文件的 R 包。

## 栗子

下面这个示例绘制了中国及周边国家的行政区划，以及标记了北京的位置

> 数据来自中科院地理所：<https://www.resdc.cn/data.aspx?DATAID=205>

```R
library(sf)
library(ggplot2)

world_map_data <- st_read("rawdata/世界国家.shp")
wm_geom <- st_geometry(world_map_data)

png("map.png")
ggplot() +
    geom_sf(data = wm_geom) +
    geom_point(aes(x = 116, y = 40), shape = 2, fill = "red", color = "red") +
    scale_x_continuous(limits = c(70, 140)) +
    scale_y_continuous(limits = c(0, 55))
dev.off()

```