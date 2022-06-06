---
title: "Simple Features for R"
tags:
    - R
    - Geographic
---

[sf](https://r-spatial.github.io/sf/index.html) 包是一个用于读取和操作一些地理向量型数据的 R 包。

## 读写数据
`st_read` 函数：读取 shapefile

```r
# 读取 shapefile 的第一个 layer
countries <- st_read("rawdata/世界国家.shp")
# 读取名为“世界国家”的 layer
countries <- st_read("rawdata/世界国家.shp", "世界国家")
```

`st_layers` 函数：列出 shapefile 的 layer
```r
st_layers("rawdata/世界国家.shp")
```

`st_write` 函数：将 sf 对象写入 shapefile
```r
st_write(countries, "world.shp", layer_options = "ENCODING=UTF-8")
```

## sf 对象
`st_as_df` 函数：将一个 data.frame 转换为 sf 对象
```r
new_sf <- st_as_sf(
    df_with_coord,
    coords = c("Long", "Lat"),
    agr = "constant",
    crs = "+proj=longlat +datum=WGS84",
    stringsAsFactors = FALSE,
    remove = TRUE
)
```

`st_join` 函数：合并 sf 对象。[^1]
```r
# 获得 ssw_sf 数据点所在的国家信息
accession_in_countries <- st_join(ssw_sf, countries, join = st_within)
```

`st_centroid`  函数：计算多边形的中心点坐标。
```r
countries_centroid <- st_centroid(countries)
```

`st_coordinates` 函数：将几何图形的坐标解析成矩阵。
```r
x_y_matrix <- st_coordinates(countries_centroid)
```

## 绘图

下面这个示例绘制了中国及周边国家的行政区划，以及标记了北京的位置。（数据来自中科院地理所[^2]）

```R
library(sf)
library(ggplot2)

countries <- st_read("rawdata/世界国家.shp")
wm_geom <- st_geometry(countries)

png("map.png")
ggplot() +
    geom_sf(data = wm_geom) +
    geom_point(aes(x = 116, y = 40), shape = 2, fill = "red", color = "red") +
    scale_x_continuous(limits = c(70, 140)) +
    scale_y_continuous(limits = c(0, 55))
dev.off()

```

[^1]: [POINT-IN-POLYGON WITH SF](https://mattherman.info/blog/point-in-poly/)
[^2]: [全球国家行政边界数据](https://www.resdc.cn/data.aspx?DATAID=205)