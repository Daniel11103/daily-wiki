# network

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 从源码编译安装 StrongSwan

*2023-09-04* <span class="kb-pill">#网络</span> <span class="kb-pill">#VPN</span>

> StrongSwan 是 IPsec 的开源实现，按 autotools 方式从源码编译安装。

**步骤**

1. 下载并解压：`tar xjf strongswan-x.x.x.tar.bz2`，进入目录
2. 配置：`./configure --prefix=/usr --sysconfdir=/etc`，可按需添加其他选项
3. 编译安装：`make`，然后 `sudo make install`

**说明**：原文示例包含完整的 IPsec 连接配置，需根据实际环境修改。

</div>

<div class="kb-card" markdown="1">

## PPPoE 拨号的工作流程

*2021-12-29* <span class="kb-pill">#网络</span> <span class="kb-pill">#PPPoE</span>

> PPPoE 分为发现阶段和会话阶段：先通过无状态的发现获得对端 MAC 并建立会话 ID，再进入标准 PPP 会话。

**发现阶段**

1. PADI：主机广播发起请求
2. PADO：接入集中器响应
3. PADR / PADS：主机请求，集中器确认并分配 Session-ID

**会话阶段**

- 使用确定的 Session-ID 进入标准 PPP 会话，完成认证和地址分配

</div>

<div class="kb-card" markdown="1">

## IPv6 报文头与 IPv4 的主要区别

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#IPv6</span>

> IPv6 的以太网类型为 `0x86dd`，报文头固定 40 字节，处理效率更高。

**要点**

- 固定 40 字节头部，IPv4 头部为变长
- Hop Limit 作用类似 IPv4 的 TTL
- Traffic Class 作用类似 IPv4 的 TOS
- 取消了头部校验和字段，减轻路由器逐跳处理的负担

</div>

<div class="kb-card" markdown="1">

## 用 ping 测试路径 MTU

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#MTU</span>

> 以太网 MTU 默认 1500，IP 头 20 字节、ICMP 头 8 字节，因此 ping 的数据长度最大为 1472。

**步骤**

1. 禁止分片发送：`ping -M do -s 1472 <目标地址>`（Linux）
2. 若提示需要分片，则逐步减小 `-s` 的值，直到通过为止，此时 MTU = 数据长度 + 28

</div>

<div class="kb-card" markdown="1">

## DNS 解析的层级结构

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#DNS</span>

> DNS 按层级查找域名：根域 → 顶级域 → 权威域名服务器。

**要点**

- 根域用 `.` 表示，全球有 13 个根服务器地址，通过任播技术分布在多个镜像站点
- 顶级域分为按行业划分（`com`、`net`）和按国家划分（`cn`、`jp`）两类
- 每个域都有权威域名服务器，负责解析该域内的记录，如 `www.example.com` 由 `example.com` 的权威服务器解析

</div>

<div class="kb-card" markdown="1">

## TCP 三次握手与四次挥手

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#TCP</span>

> TCP 建立连接需要三次握手，断开连接需要四次挥手。

**三次握手**

1. 客户端发送 SYN
2. 服务器回复 SYN-ACK
3. 客户端回复 ACK，连接建立

**四次挥手**

- 双方各发送一次 FIN 并确认，连接关闭

</div>

<div class="kb-card" markdown="1">

## Netplan 静态 IP 配置示例

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#netplan</span>

> Ubuntu 使用 netplan 在 `/etc/netplan/*.yaml` 中配置网络。

**示例**
```yaml
network:
  version: 2
  ethernets:
    eth0:
      addresses: [<IP地址>/24]
      routes:
        - to: default
          via: <网关地址>
      nameservers:
        addresses: [<DNS地址>]
```

**步骤**：编辑文件后执行 `sudo netplan try` 测试，确认无误再 `sudo netplan apply`。

</div>

<div class="kb-card" markdown="1">

## 配置 IGMP Snooping 组播路由端口

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#组播</span>

> 在交换机上静态指定连接组播路由器的端口。

**步骤**

1. 进入全局配置模式：`configure terminal`
2. `ip igmp snooping vlan <vlan-id> mrouter interface <接口>`
3. 查看结果：`show ip igmp snooping mrouter [vlan <vlan-id>]`
4. 保存：`copy running-config startup-config`

**说明**：静态组播路由端口只支持在设备物理端口上配置。

</div>

<div class="kb-card" markdown="1">

## H3C 交换机配置 Q-in-Q 基础

*未标注* <span class="kb-pill">#网络</span> <span class="kb-pill">#vlan</span>

> Q-in-Q 在报文外层再加一层 VLAN 标签，用于扩展 VLAN 范围。

**步骤**

1. 全局开启：`qinq enable`
2. 定义流行为并添加外层标签：`traffic behavior <名称>`，再 `nest top-most vlan-id <外层VLAN>`
3. 在端口上透传指定 VLAN：`qinq transparent-vlan <vlan-list>`

</div>
