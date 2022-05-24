## 安装Docker

### 一、安装Docker CE本体

````bash
# step 1: 安装必要的一些系统工具
sudo apt update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
# step 2: 安装GPG证书
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# Step 3: 写入软件源信息（此处的软件源只是Docker CE的软件源，不是Docker Hub的镜像）
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# Step 4: 更新并安装Docker-CE
sudo apt-get -y update
sudo apt-get -y install docker-ce
````

至此Docker CE就安装好了。

### 二、使用阿里云的容器镜像服务

首先，在控制台中找到“容器镜像服务”，进入并设置Registry密码。  
然后，在终端中登录。  

````bash
sudo docker login --username=阿里云用户名 registry.cn-beijing.aliyuncs.com
````

最后，修改``/etc/docker/daemon.json``来使用加速器。

````bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["加速器地址"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
````

至此，加速器就配置好了。

### 其他

### 1. 安装docker-compose

````bash
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-`uname -s`-`uname -m`" > /usr/local/bin/docker-compose
````

(阿里云从github下载东西会很慢)

## Docker基本操作

本篇记录了些常见的Docker命令的用法。

### 进入容器

命令：``docker exec -it MYCONTAINER /bin/bash``  
该命令可以进入到容器内并运行其中的bash。  

- ``-i``：使得容器内的bash能够接受我们的输入。
- ``-t``：提供一个伪终端提示符。

### 用Docker安装Nginx

首先，获取Nginx的镜像。

````bash
docker image pull nginx
````

然后，创建一个Docker的Volume，用来存放Nginx的网页文件和配置文件。

````bash
docker volume create mynginxhtml
docker volume create mynginxconfig
````

查看一下volume的绝对位置。

````bash
docker volume inspect mynginxhtml mynginxconfig
````

回显内容如下：

````bash
[
    {
        "CreatedAt": "2020-10-08T15:52:53+08:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/mynginxhtml/_data",
        "Name": "mynginxhtml",
        "Options": {},
        "Scope": "local"
    },
    {
        "CreatedAt": "2020-10-08T15:52:53+08:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/mynginxconfig/_data",
        "Name": "mynginxconfig",
        "Options": {},
        "Scope": "local"
    }
]
````

其中，``"Mountpoint"``所指的就是volume的绝对位置。

### 安装Nginx

````bash
docker container run -d \
    -p 80:80 \
    -v mynginxhtml:/usr/share/nginx/html/ \
    -v mynginxconfig:/etc/nginx \
    --name mynginx \
    nginx
````

- ``-d``：在后台运行；
- ``-p``：冒号左侧是本机端口，冒号右侧是要映射的容器端口；
- ``-v``或``--volume``：冒号左侧是Docker的Volume的名字，冒号右侧是要映射的容器的位置；
- ``--name``：安装的container的名字；
- 最后跟上要安装的image的名字。


## 参考

1. <https://edu.aliyun.com/course/426>
2. <https://docs.docker.com/engine/install/ubuntu/>
3. <https://developer.aliyun.com/mirror/docker-ce>
4. <https://cr.console.aliyun.com/cn-beijing/instances/mirrors>
