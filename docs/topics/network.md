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
