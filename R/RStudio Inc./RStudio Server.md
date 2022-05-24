## 安装 RStudio Server

这里记录了在 CentOS7 中安装 RStudio Server 的过程。

首先要安装 R，按照[官网的教程](https://docs.rstudio.com/resources/install-r/)即可

```bash
# Enable the Extra Packages for Enterprise Linux (EPEL) repository
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# Specify R version
export R_VERSION=4.1.2

# Download and install R
curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
sudo yum install R-${R_VERSION}-1-1.x86_64.rpm

# Create a symlink to R
sudo ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R
sudo ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript
```

之后再按照[官网的教程](https://www.rstudio.com/products/rstudio/download-server/redhat-centos/)安装 RStudio Server

```bash
wget https://download2.rstudio.org/server/centos7/x86_64/rstudio-server-rhel-2021.09.1-372-x86_64.rpm
sudo yum install rstudio-server-rhel-2021.09.1-372-x86_64.rpm
```

## 设置 RStudio Server 不自动注销

按照 RStudio Server 的默认设置，在用户关闭浏览器一段时间后，服务器端就会暂停用户的会话。当用户再次打开 RStudio Server 的页面时就又需要输入账号密码了。

通过修改 RStudio Server 的配置文件 ``/etc/rstudio/rserver.conf``，在其中添加以下语句。

```txt
auth-timeout-minutes=0
auth-stay-signed-in-days=30
```

保存退出后重启 RStudio Server。

```bash
sudo rstudio-server restart
```

再重新通过浏览器登录 RStudio Server 时，勾选框旁边的说明文字就变了。

参考：<https://github.com/rstudio/rstudio/issues/5449#issuecomment-637586731>