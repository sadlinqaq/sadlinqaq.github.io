---
title: 'linux部署'
description: 'linux和docker的一些学习笔记..'
publishDate: '2026-05-13 22:25:24'
tags:
  - Linux
  - Docker
  - 服务器
heroImage: { src: './thumbnail.png', alt: 'an image targeting my article', color: '#B6E6FA' }
---

# <span style="color:#FF9A00">Linux</span>
是一套开源免费、稳定安全、多用户多任务的类 Unix 操作系统，广泛用于服务器、嵌入式、云计算与开发环境。

## <span style="color:#FF00FF">CentOS</span>
是基于 Red Hat Enterprise Linux（RHEL） 源码构建、免费开源、高度兼容 RHEL 的企业级 **Linux 发行版**，主打稳定、长期支持、安全，曾是服务器领域最主流选择之一。

## <span style="color:#FFF700">VMware Workstation</span>
VMware Workstation Pro 是业界主流的桌面虚拟化软件（Type 2 型 Hypervisor），可在 Windows/Linux 主机上同时运行多台虚拟机（VM），支持 Windows、Linux、macOS 等系统，2024 年 11 月起对个人与商业用户完全免费。

## 虚拟服务器
* 在**VMware Workstation**配置虚拟网卡,设置网段
* 将**CentOS**安装在**VMware Workstation**
* 进入虚拟机通过命令行：**ip addr** 查看ip地址

## <span style="color:#21AAEF">FinalShell</span>
是国产、跨平台、免费的一体化服务器管理工具，集 SSH 终端、SFTP 文件传输、服务器监控、批量管理 于一体，是连接管理 CentOS 等 Linux 服务器的首选工具。

* 将服务器的ip地址输入并登录实现远程管理

## <span style="color:#FF9A00">Linux</span> 目录
根目录 "/"
* bin 存放二进制可执行文件
* boot 存放系统引导时使用的各种文件
* dev 存放设备文件
* **etc 存放系统配置文件**
* home 存放系统用户文件
* lib 存放程序运行所需的共享库和内核模块
* opt 额外安装的可选应用程序包所放置的位置
* **root 超级用户目录**
* sbin 存放二进制可执行文件，只有root用户可以访问
* tmp 临时文件
* **usr 存放系统应用程序**
* var 存放运行时需要改变数据的文件，如日志文件

## <span style="color:#FF9A00">Linux</span> 常用命令

### <span style="color:green">Linux 命令格式</span> 
```
command [-options] [parameter]
```
**说明**
* command: 命令名
* [-options]：选项，可用来对命令进行控制，可省略
* [parameter]：参数，可以是任意个

**查看详细命令**
```
command --help
```

**其他命令**
```
pwd 查看当前目录路径
clear 清屏
```


### <span style="color:green">目录操作命令</span>
#### 显示指定目录的内容
```
ls [-al] [dir]
```
* -a: 显示文件以及目录（包括隐藏文件）
* -l: 除文件名外，同时将文件类型（d表示目录，-表示文件）、权限、拥有者、文件大小等信息详细列出（简写为**ll**）

#### 切换当前工作目录
```
cd [dirName]
```

#### 创建目录
```
mkdir [-p] dirName
```
* -p: 确保存在，不存在则创建（多级目录创建）

#### 删除文件或者目录
```
rm [-rf] name 
```
* -r: 将目录以及目录中的文件逐一删除，即递归删除
* -f：无需确认，直接删除

### <span style="color:green">文件操作命令</span>
#### 显示文件所有内容
```
cat [-n] fileName
```
* -n: 由1开始对所有输出的行数编号

#### 以分页形式显示文件内容
```
more fileName
```
**操作说明**
* 回车键：向下滚动一行
* 空格键：向下滚动一屏
* b：返回上一屏
* q或ctrl+c：退出more

#### 查看文件开头内容
默认十行内容
```
head [-n] fileName
```
* -n: 输出文件开头n行内容

#### 查看文件末尾内容
默认十行内容
```
tail [-nf] fileName
```
* -n: 输出文件末尾n行内容
* -f： 动态读取文件尾部内容

### <span style="color:green">拷贝移动命令</span>
#### 复制文件或目录
```
cp [-r] source(被复制的文件) dest(/root/...)
```
* -r: 复制该目录下的所有子目录与文件

#### 重命名或移动文件或目录
```
mv source dest
```
第二个参数如果是已存在的目录执行移动

### <span style="color:green">打包压缩命令</span>
#### 对文件进行打包、解包、压缩、解压
```
tar [-zcxvf] fileName(操作后的名字，.tar/.tar.gz) [files](需要操作的文件)
```
* 文件后缀为.tar表示完成打包
* 文件后缀为.tar.gz表示打包的同时还进行了压缩
* -z: 压缩或者解压
* -c: 打包
* -x：解包
* -v：显示命令执行过程
* -f: 指定包文件的名称

### <span style="color:green">文本编辑命令</span>
#### vi编辑器
**linux**系统自带的文本编辑工具，类似**Windows**的记事本
```
vi fileName
```
#### <span style="color:#001AFF">vim</span>编辑器
**vi**的增强版,编辑文件时可以对文本内容进行着色
* 用**yum**命令安装
```
yum install vim
```
* <span style="color:#001AFF">vim</span>语法
```
vim fileName
```

* esc: 命令模式
  * gg: 定位到第一行
  * G：定位到最后一行
  * dd: 删除一行
  * u: 撤销操作
  * ndd: 删除n行数据
* i,a,o: 插入模式
* **:**: 底行模式
  * wq: 保存并退出
  * q!: 不保存退出
  * set nu: 设置行号
  * set nonu: 取消行号
  * n: 定位到n行

### <span style="color:green">查找命令</span>
#### 指定目录查找文件
```
find dirName(指定目录) -option(-name) fileName("*.log")
```
* -option: 根据属性查找

#### 指定文件查找内容
```
grep [-inAB] word(查找目标) fileName(指定文件)
```
* -i: 忽略大小写
* -n: 显示关键字的行号
* -An: 显示关键字出现的前n行
* -Bn: 显示关键字出现的后n行

## <span style="color:blue">docker</span> 
是一个开源的容器化平台，核心是把应用 + 依赖 + 环境打包成可移植的容器，实现 “一次构建、处处运行”，是云原生与微服务的基础技术。

### <span style="color:blue">docker</span> 安装（CentOS 7）
#### 对 Centos 7 进行换源处理，选用阿里的yum源
* 在root用户下输入 **cd /etc/yum.repos.d** 命令
* 输入**cp CentOS-Base.repo CentOS-Base.repo.back**将CentOS-Base.repo 进行备份
* 在root用户下输入命令 **curl -o /etc/yum.repos.d/CentOS-Base.repo​ http://mirrors.aliyun.com/repo/Centos-7.repo** ,下载阿里云的 CentOS 7 软件源配置文件
* 完成后输入命令 **yum clean all**,清理旧的 yum 缓存
* 完成后输入命令 **yum makecache** 直至数据加载完成,重新生成新的软件源缓存
* 完成后输入命令 **yum update -y** 更新安装包 直至完成,更新系统所有可更新的软件包
* 最后在root用户下输入命令 **yum install wget** 安装wget软件,方便后续下载文件。

#### 安装docker
* 安装依赖
```
  sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
* 添加 Docker 源
```
  sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
* 安装 Docker
```
  sudo yum install -y docker-ce docker-ce-cli containerd.io
```
* 启动并设置开机自启
```
systemctl start docker
systemctl enable docker
```
* 验证**docker --version**
* 配置国内镜像加速
```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
    "http://hub-mirror.c.163.com",
    "https://mirrors.tuna.tsinghua.edu.cn",
    "http://mirrors.sohu.com",
    "https://ustc-edu-cn.mirror.aliyuncs.com",
    "https://ccr.ccs.tencentyun.com",
    "https://docker.m.daocloud.io",
    "https://docker.awsl9527.cn"
  ]
}
EOF
```
* 重启 Docker：
```
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 镜像
当我们利用docker安装应用时，docker会自动搜索（镜像仓库[Docker Hub](http://hub.docker.com/)）并下载镜像（image）,镜像不只包含应用本身，还包含所需要的环境、配置、系统函数库。

### 容器
docker在运行镜像时创建一个隔离环境，成为容器。

### docker run 命令解读
```
docker run -d \ 
  --name mysql \
  -p 3307:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  mysql:8
```
* docker run : 创建并运行一个容器，-d 后台运行
* --name : 给容器取名字
* -p : 设置端口映射
* -e : 设置环境变量
* mysql:8 : 指定运行镜像的名字，版本（[repository]:[tag]）不写版本默认最新

### 常见命令
* docker pull
拉取镜像
* docker images
查看镜像
* docker rmi
删除镜像
* docker build
自定义镜像
* docker save
打包镜像
* docker push
推送镜像到镜像仓库（需要合法权限）
* docker run
创建并运行镜一个容器
* docker stop
停止容器
* docker start
启动容器
* docker ps
查看运行的容器
* docker rm
删除容器
* docker logs
查看容器日志
* docker exec
进入容器内部

### 数据卷（volume）
是一个虚拟目录，是**容器内目录**与**宿主机目录**之间的映射桥梁

#### 数据卷指令 docker volume --help

#### 创建数据卷
以nginx为例，在创建容器时就创建数据卷
```
docker run -d --name nginx -p 80:80 -v html:/usr/share/nginx.html nginx:1.20.2
```
* -v html:/usr/share/nginx.html
创建的数据卷：映射容器内的目录
* -v /root/XXX/..:/usr/share/nginx.html
本地目录挂载 

### 自定义镜像
* Dockerfile
是一个文本文件，包含一个个指令，指令说明执行什么操作构建镜像。

|指令|说明|示例|
|:---:|:---:|:---:|
|FROM|指定基础镜像|FROM centos:7|
|ENV|设置环境变量|ENV key=value|
|COPY|拷贝本地文件到镜像指定目录|COPY ./jdk.tar.gz/tmp|
|RUN|执行Linux的shell命令|RUN tar -zxvf /tmp/jdk17.tar.gz|
|EXPOSE|指定容器的监听端口|EXPOSE 8080|
|ENTRYPOINT|镜像中应用的启动命令|ENTRYPOINT java -jar xx.jar|
* 编写好Dockerfile文件后，利用下面命令构建镜像
```
docker build -t myImage:1.0 .
```
-t : 起名
. : 指定Dockerfile文件所有目录，当前目录为"."

### 自定义网络
#### 命令
|命令	|说明|
|:---:|:---:|
|docker network create	|创建一个网络
|docker network ls|	查看所有网络
|docker network rm|	删除指定网络
|docker network prune	|清除未使用的网络
|docker network connect|	使指定容器连接加入某网络
|docker network disconnect|	使指定容器连接离开某网络
|docker network inspect|	查看网络详细信息

### DockerCompose
通过一个配置文件（.xml），把整套环境一起启动 

#### DockerCompose命令
* 命令格式
```
docker compose [OPTIONS] [COMMAND]
```
* 参数选择

|类型|	参数或指令	|说明|
|:---:|:---:|:---:|
|Options|	-f|	指定 compose 文件的路径和名称|
|Options	|-p|	指定 project 名称|
|Commands|	up|	创建并启动所有 service 容器|
|Commands|	down|	停止并移除所有容器、网络|
|Commands|	ps	|列出所有启动的容器|
|Commands|	logs|	查看指定容器的日志|
|Commands|	stop|	停止容器|
|Commands|	start|	启动容器|
|Commands|	restart|	重启容器|
|Commands|	top|	查看运行的进程|
