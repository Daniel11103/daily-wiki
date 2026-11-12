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
