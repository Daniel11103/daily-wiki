# openvswitch

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 查看 OVS 网桥和端口

*未标注* <span class="kb-pill">#openvswitch</span> <span class="kb-pill">#网络</span>

> 用 `ovs-vsctl` 查看网桥、端口及其配置。

**常用命令**

- 查看所有网桥：`ovs-vsctl list-br`
- 查看某网桥的端口：`ovs-vsctl list-ports <网桥名>`
- 查看完整拓扑：`ovs-vsctl show`

</div>

<div class="kb-card" markdown="1">

## OVS 端口的 VLAN 模式

*未标注* <span class="kb-pill">#openvswitch</span> <span class="kb-pill">#vlan</span>

> 通过 `vlan_mode` 设置端口的 VLAN 行为，类似交换机的 trunk 和 access 配置。

**设置**
`ovs-vsctl set port <端口名> vlan_mode=trunk|access|native-tagged|native-untagged`

**模式说明**

- `trunk`：传递指定 VLAN（由 `trunks` 指定）的报文，未指定时放行所有 VLAN
- `access`：只允许属于 `tag` 指定 VLAN 的报文通过，并去掉标签
- `native-tagged` / `native-untagged`：指定原生 VLAN 是否携带标签

</div>

<div class="kb-card" markdown="1">

## 用 ovs-ofctl 查看与操作流表

*未标注* <span class="kb-pill">#openvswitch</span> <span class="kb-pill">#流表</span>

> `ovs-ofctl` 用于查看和管理 OpenFlow 流表。

**常用命令**

- 查看流表：`ovs-ofctl dump-flows <网桥>`
- 查看聚合统计：`ovs-ofctl dump-aggregate <网桥>`
- 查看端口信息：`ovs-ofctl show <网桥>`

**流表组成**：每条规则由基础字段（cookie、duration、table、priority）、匹配字段和动作字段组成。

</div>
