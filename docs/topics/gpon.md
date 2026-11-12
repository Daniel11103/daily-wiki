# gpon

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## GPON 网络工作原理

*未标注* <span class="kb-pill">#gpon</span> <span class="kb-pill">#网络</span>

> GPON 用一根光纤连接 OLT、分光器和 ONU，下行广播、上行分时发送。

**要点**

- 上行波长 1290–1330nm，下行波长 1480–1500nm，通过波分复用在同一网络上传输
- 下行：OLT 向所有 ONU 广播，ONU 根据 gemport ID 过滤出属于自己的数据
- 上行：ONU 只能在 OLT 分配的时隙内发送数据（TDMA），避免冲突

</div>

<div class="kb-card" markdown="1">

## GPON 基本设备概念

*未标注* <span class="kb-pill">#gpon</span> <span class="kb-pill">#概念</span>

> GPON 网络的三类核心设备及其位置。

- **GPON**：吉比特无源光网络（Gigabit passive optical network）
- **OLT**：光线路终端，通常放在中心机房
- **ONU/ONT**：光网络单元或终端，放在用户侧

</div>
