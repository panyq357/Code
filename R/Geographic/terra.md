---
title: terra
author: panyq
tags:
    - R
    - Geographic
---

terra 包是用于对地理数据进行读写操纵的 R 包，它是旧的 raster 包的继任者。

[terra 包的文档](https://rspatial.org/terra/spatial/index.html)

## 读取数据
`vect` 函数：读取 Vector 型数据，比如 shapefile（一套 shapefile 数据包含`.shp`, `.shx`, `.dbf`，以及可选的 `.prj` 文件）。（更推荐使用 [[sf]] 包）
```r
political_map <- vect("rawdata/世界国家.shp")
```

`vect` 函数也可用于创建 SpatVector 对象。
```r
xy <- ssw %>% select(Long, Lat) %>% as.matrix() %>% vect()
```

`rast` 函数：读取 Raster 型数据，比如 GeoTIFF（`.tif` 文件）。
```r
nitro_5000m_0_5cm <- rast("rawdata/nitrogen_0-5cm_mean_5000.tif")
```

## Coordinate Reference Systems
`crs` 函数：查看和修改数据的 CRS。
```r
crs(pp) <- "+proj=longlat +datum=WGS84"
crs(xy) <- crs(nitro_longlat)
```

`project` 函数：转换 CRS。
```r
newcrs <- "+proj=robin +datum=WGS84"
rob <- project(p, newcrs)
```

## 提取数据
`buffer` 函数：获取 SpatVector 中几何图形周边的缓冲区。（需要有 CRS）
```r
xy_buffer <- buffer(
    xy,
    width = 45000  # 缓冲区范围（当 CRS 是 longlat 时，单位为米）
)
```

`extract` 函数：提取坐标附近的方格的数据。
```r
nitro_value <- terra::extract(nitro_longlat, xy_buffer, fun = "mean", na.rm = T) %>%
    pull(2)
```