# ssh

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 配置 SSH 免密码登录

*2021-07-15* <span class="kb-pill">#ssh</span> <span class="kb-pill">#安全</span>

> 生成密钥对，并把公钥复制到目标主机，之后即可免密码登录。Windows 需先安装 Git Bash。

**步骤**

1. 生成密钥对：`ssh-keygen -t rsa`，生成在 `~/.ssh/` 目录下
2. 复制公钥到目标主机：`ssh-copy-id user@<目标IP>`

**说明**：`id_rsa` 是私钥，`id_rsa.pub` 是公钥，只把公钥复制给目标主机。

</div>
