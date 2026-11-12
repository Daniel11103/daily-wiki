# linux

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 按进程名批量结束进程

*2023-02-10* <span class="kb-pill">#linux</span> <span class="kb-pill">#进程</span>

> 按进程名批量结束进程，无需逐个查找 PID。

**步骤**

1. 取出匹配进程的 PID：`ps -e | grep python3 | awk '{print $1}'`
2. 交给 kill 结束：`ps -e | grep python3 | awk '{print $1}' | xargs kill -9`

**说明**：将 `python3` 替换为你要结束的进程关键字。

</div>

<div class="kb-card" markdown="1">

## 设置主机的 FQDN

*2023-11-01* <span class="kb-pill">#linux</span> <span class="kb-pill">#网络</span>

> FQDN 是主机名加域名，例如 `www.example.com`。Linux 没有直接设置 FQDN 的命令，需要通过 hostname 和 hosts 文件配合完成。

**步骤**

1. 编辑 `/etc/hostname`，写入主机名，例如 `elk`
2. 编辑 `/etc/hosts`，添加一行：`<IP> <FQDN> <主机名>`，例如 `192.168.x.x elk.example.com elk`
3. 执行 `hostname -F /etc/hostname` 更新主机名
4. 执行 `hostname -f` 查看 FQDN，`hostname` 查看主机名

</div>

<div class="kb-card" markdown="1">

## 用 Systemback 备份和还原系统

*2026-01-09* <span class="kb-pill">#linux</span> <span class="kb-pill">#备份</span>

> Systemback 可以备份还原系统，并制作启动盘和 ISO 镜像。原项目已停止维护，改进版支持 Ubuntu 20.04。

**步骤**

1. 按原文添加 Systemback 的软件源和签名密钥，然后执行 `sudo apt-get update` 和 `sudo apt-get install systemback`
2. 分区建议：EFI 分区不小于 512MiB，其余空间分配给根目录 `/`

**说明**：改进版已支持大文件，生成的 ISO 不再受 4GB 限制。

</div>

<div class="kb-card" markdown="1">

## 用 systemd 实现虚拟机开机自启

*2025-08-18* <span class="kb-pill">#linux</span> <span class="kb-pill">#虚拟化</span>

> 为每台 VirtualBox 虚拟机生成一个 systemd 服务，系统开机后自动启动它们。

**步骤**

1. `VBoxManage list vms` 查看虚拟机名称（区分大小写）
2. 编写脚本，为每台虚拟机生成 systemd 服务文件，参数包括运行用户、启动延迟秒数和虚拟机名
3. 执行 `systemctl daemon-reload` 后用 `systemctl enable` 设为开机启动

**说明**：虚拟机需以普通用户运行，服务中要指定该用户。

</div>

<div class="kb-card" markdown="1">

## 解决 XRDP 远程桌面黑屏

*2024-05-28* <span class="kb-pill">#linux</span> <span class="kb-pill">#远程桌面</span>

> Ubuntu 20.04 安装 XRDP 后远程连接可能黑屏，修改启动脚本即可解决。

**步骤**

1. `sudo apt install xrdp` 安装，`sudo adduser xrdp ssl-cert` 将 xrdp 加入证书组，`sudo systemctl restart xrdp` 重启服务
2. 编辑 `/etc/xrdp/startwm.sh`，添加 `unset DBUS_SESSION_BUS_ADDRESS` 和 `unset XDG_RUNTIME_DIR`
3. 保存后重新连接远程桌面

</div>

<div class="kb-card" markdown="1">

## 设置或修改系统时区

*2023-07-17* <span class="kb-pill">#linux</span> <span class="kb-pill">#时间</span>

> 系统时区影响 cron 定时任务和日志时间戳，可用 `timedatectl` 查看和修改。

**步骤**

1. `timedatectl` 查看当前时区
2. `sudo timedatectl set-timezone <时区>` 修改，例如 `Asia/Shanghai`

</div>

<div class="kb-card" markdown="1">

## 用 ss 代替 netstat 查看连接

*2022-07-19* <span class="kb-pill">#linux</span> <span class="kb-pill">#网络</span>

> `ss` 显示 socket 状态，速度比 `netstat` 快，并支持按状态和地址过滤。

**步骤**

1. 统计已建立的连接数：`ss -o state established | wc -l`，替代 `netstat -ant | grep EST | wc -l`
2. 按地址过滤：`ss src <IP>`，按端口过滤：`ss src <IP>:80`

</div>
