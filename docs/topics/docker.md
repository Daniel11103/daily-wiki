# docker

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 管理镜像仓库：登录、拉取与推送

*2023-06-13* <span class="kb-pill">#docker</span> <span class="kb-pill">#镜像</span>

> 通过 Docker Hub 等仓库存取镜像，推送前需先登录账号。

**步骤**

1. 登录：`docker login`，退出：`docker logout`
2. 搜索：`docker search ubuntu`
3. 拉取：`docker pull ubuntu`
4. 推送：先打标签，再推送
   - `docker tag ubuntu:18.04 username/ubuntu:18.04`
   - `docker push username/ubuntu:18.04`

**说明**：将 `username` 替换为你自己的 Docker 账号。

</div>

<div class="kb-card" markdown="1">

## 导出与导入镜像

*2023-08-17* <span class="kb-pill">#docker</span> <span class="kb-pill">#镜像</span>

> 用 `save` 把镜像导出为 tar 文件，再用 `load` 导入。

**步骤**

1. 导出：`docker save -o my_ubuntu_v3.tar runoob/ubuntu:v3`
2. 导入：`docker load -i my_ubuntu_v3.tar`

</div>

<div class="kb-card" markdown="1">

## 用 Dockerfile 定制镜像

*2023-05-26* <span class="kb-pill">#docker</span> <span class="kb-pill">#镜像</span>

> Dockerfile 是描述镜像构建步骤的文本文件，`docker build` 按指令逐层生成镜像。

**步骤**

1. 新建目录和 `Dockerfile`，用 `FROM` 指定基础镜像
2. 用 `RUN` 执行构建命令，例如：`RUN echo '内容' > /usr/share/nginx/html/index.html`
3. 在该目录执行 `docker build -t <名称>:<标签> .` 构建镜像

**注意**：每条 `RUN` 都会新增一层，用 `&&` 合并多条命令可减少镜像层数。

</div>

<div class="kb-card" markdown="1">

## 用 Docker Compose 编排多容器应用

*2020-11-23* <span class="kb-pill">#docker</span> <span class="kb-pill">#编排</span>

> Compose 通过 `docker-compose.yml` 定义多个服务，一条命令即可启动整套应用。

**步骤**

1. 用 Dockerfile 定义应用运行环境
2. 在 `docker-compose.yml` 的 `services` 中定义各服务，例如 web、redis
3. 执行 `docker-compose up` 启动全部服务

**说明**：Linux 可从 GitHub Releases 下载对应版本的二进制文件，放到 `/usr/local/bin/` 并添加执行权限。

</div>

<div class="kb-card" markdown="1">

## 搭建 Swarm 集群

*2020-11-23* <span class="kb-pill">#docker</span> <span class="kb-pill">#集群</span>

> Swarm 把多台 Docker 主机组成一个集群，manager 负责管理，worker 负责运行任务。

**步骤**

1. 在管理节点执行 `docker swarm init --advertise-addr <管理节点IP>`
2. 在工作节点执行初始化输出中的 `docker swarm join --token <token> <管理节点IP>:2377`

**注意**：join 命令中的 token 是凭据，不要公开或提交到代码仓库。

</div>

<div class="kb-card" markdown="1">

## 用 Docker Machine 管理远程主机

*2024-01-04* <span class="kb-pill">#docker</span> <span class="kb-pill">#工具</span>

> Docker Machine 可以在虚拟机或云主机上安装并集中管理 Docker。

**步骤**

1. 先在本机安装 Docker
2. 使用 `docker-machine create -d <驱动> <主机名>` 创建主机，例如驱动 `virtualbox`
3. 使用 `docker-machine` 命令启动、检查、停止和重启托管主机

**说明**：支持本地虚拟机，也支持阿里云、腾讯云、AWS、DigitalOcean 等云供应商。

</div>

<div class="kb-card" markdown="1">

## 迁移 Docker 数据目录到大容量磁盘

*2023-01-04* <span class="kb-pill">#docker</span> <span class="kb-pill">#磁盘</span>

> 默认数据目录 `/var/lib/docker` 位于系统盘，空间不足时可迁移到大容量磁盘。

**步骤**

1. `df -h` 查看各磁盘容量，`du -sh /var/lib/docker/` 查看 Docker 占用
2. `systemctl stop docker` 停止服务
3. 将数据目录迁移到大容量磁盘，并在 `/etc/docker/daemon.json` 中通过 `data-root` 指向新目录
4. `systemctl start docker` 启动服务并验证

**注意**：原文作者在执行 systemctl 时遇到过启动失败的报错，操作前先确认服务状态。

</div>

<div class="kb-card" markdown="1">

## 将运行中的容器打包为镜像

*2023-10-07* <span class="kb-pill">#docker</span> <span class="kb-pill">#镜像</span>

> 使用 `docker commit` 把容器当前的状态保存为新镜像。

**步骤**

1. `docker ps -a` 查看容器列表和容器 ID
2. `docker commit [OPTIONS] <容器> [仓库[:标签]]` 生成镜像

**说明**：`commit` 保存的是容器当前的文件系统状态，不包含挂载的数据卷内容。

</div>

<div class="kb-card" markdown="1">

## 容器的基本操作

*2023-07-18* <span class="kb-pill">#docker</span> <span class="kb-pill">#容器</span>

> 拉取镜像、启动交互式容器，并查看所有容器状态。

**步骤**

1. `docker pull ubuntu` 拉取镜像
2. `docker run -it ubuntu /bin/bash` 启动并进入容器（`-i` 交互，`-t` 终端）
3. 在容器内输入 `exit` 退出
4. `docker ps -a` 查看所有容器，包括已停止的

</div>
