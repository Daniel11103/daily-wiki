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
