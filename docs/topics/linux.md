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

<div class="kb-card" markdown="1">

## 切换 Ubuntu 软件源为国内镜像

*未标注* <span class="kb-pill">#linux</span> <span class="kb-pill">#apt</span>

> 把 apt 软件源换成国内镜像，可以明显加快软件安装和更新。

**步骤**

1. 备份原配置：`sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak`
2. 编辑 `/etc/apt/sources.list`，替换为所选镜像站地址（如阿里云 `mirrors.aliyun.com/ubuntu/`），保持与系统版本代号一致（Ubuntu 20.04 为 focal）
3. 更新缓存：`sudo apt update && sudo apt upgrade`

</div>

<div class="kb-card" markdown="1">

## Ubuntu 20.04 改回传统网卡名

*未标注* <span class="kb-pill">#linux</span> <span class="kb-pill">#网卡</span>

> 通过内核参数关闭可预测网卡名，让网卡恢复为 eth0 这类名称。

**步骤**

1. 编辑 `/etc/default/grub`，在 `GRUB_CMDLINE_LINUX=""` 的引号内加入 `net.ifnames=0`
2. 重建 GRUB 配置：`sudo grub-mkconfig -o /boot/grub/grub.cfg`
3. 重启后生效

**注意**：Ubuntu 20.04 使用 netplan 管理网络，IP 配置在 `/etc/netplan/*.yaml` 中，网卡名改变后需同步修改该文件。

</div>

<div class="kb-card" markdown="1">

## 使用 minicom 连接串口设备

*未标注* <span class="kb-pill">#linux</span> <span class="kb-pill">#串口</span>

> minicom 是 Linux 下常用的串口调试工具。

**步骤**

1. 安装：`sudo apt-get install minicom`
2. 进入配置：`sudo minicom -s`，选择 Serial port setup
3. 按 `A` 设置串口设备（USB 转串口一般为 `/dev/ttyUSBx`，可用 `ls -l /dev/ttyUSB*` 确认）
4. 按 `E` 设置波特率、校验和数据位，按 `F` 关闭硬件流控
5. 保存后退出配置即可连接设备

</div>

<div class="kb-card" markdown="1">

## 树莓派搭建 Samba 共享目录

*未标注* <span class="kb-pill">#linux</span> <span class="kb-pill">#samba</span>

> 在树莓派上安装 Samba，把目录共享给局域网内的其他设备。

**步骤**

1. 安装：`sudo apt-get install samba samba-common-bin`
2. 创建共享目录并设置权限：`mkdir /home/pi/share`
3. 在 `/etc/samba/smb.conf` 末尾添加 `[share]` 段，指定 `path = /home/pi/share`
4. 添加 Samba 用户：`sudo smbpasswd -a pi`
5. 重启服务：`sudo systemctl restart smbd`

**注意**：原文使用 `chmod 777`，权限过宽，建议只开放必要的用户和读写权限。

</div>

<div class="kb-card" markdown="1">

## nano 编辑器常用快捷键

*未标注* <span class="kb-pill">#linux</span> <span class="kb-pill">#工具</span>

> nano 是 Linux 下轻量级的终端文本编辑器，底部会显示常用快捷键提示。

**常用操作**

- `Ctrl+O`：保存文件，`Ctrl+X`：退出
- `Ctrl+W`：搜索，`Ctrl+\`：搜索并替换
- `Ctrl+K`：剪切当前行，`Ctrl+U`：粘贴
- `Ctrl+G`：查看帮助

</div>
