# wireshark

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 用 text2pcap 把 hex 文本转为抓包文件

*未标注* <span class="kb-pill">#wireshark</span> <span class="kb-pill">#抓包</span>

> `text2pcap` 读取 ASCII hex 转储文本，生成 pcap 或 pcapng 文件，便于用 Wireshark 打开分析。

**步骤**

1. 进入 Wireshark 安装目录，执行 `text2pcap [选项] <输入文件> <输出文件>`
2. `-o hex|oct|dec` 指定偏移量的进制，默认为十六进制
3. `-t <时间格式>` 把行首的文本当作时间戳解析

</div>
