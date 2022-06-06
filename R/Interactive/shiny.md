## 栗子
### 下载文件
https://shiny.rstudio.com/reference/shiny/1.0.5/downloadHandler.html

### 交互式开发
将运行 shiny 的代码，和实际的 shiny app 代码分成两个文件。

```r
# app.R
library(shiny)
ui <- fluidPage(
    # Some code
)
server <- function(input, output, session) {
    # Some other code
}
shinyApp(ui, server)
```

```r
# run-shiny.R
options(shiny.autoreload = TRUE)
shiny::runApp()
```

这样只需修改 app.R 文件，然后刷新网页就能看到结果了。

### 在服务器上启动

```r
# 设置端口和 IP
options(shiny.host = "124.16.152.27")
options(shiny.port = 6756)
# 在不启动浏览器的情况下启动当前目录下 app.R 脚本里的 shiny app
shiny::runApp(launch.browser=F)
```

## 参考
- [StackOverflow 上有关在图片上进行鼠标悬浮和鼠标点击等操作的讨论](https://stackoverflow.com/questions/27965931/tooltip-when-you-mouseover-a-ggplot-on-shiny)
- [StackOverflow 上有关设置表格的列的宽度的讨论](https://stackoverflow.com/questions/25205410/r-shiny-set-datatable-column-width)
- 