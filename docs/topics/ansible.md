# ansible

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## Ansible 常用 ad-hoc 命令

*未标注* <span class="kb-pill">#ansible</span> <span class="kb-pill">#运维</span>

> 不写 playbook，直接用 `-m` 指定模块在一组主机上执行命令。

**常用示例**

- 分发文件：`ansible <主机组> -m copy -a "src=本地文件 dest=远程路径" -b -i inventory.txt`
- 远程解压：`ansible <主机组> -m unarchive -a "src=压缩包 dest=目录 copy=no" -b -i inventory.txt`
- 远程执行 shell：`ansible <主机组> -m shell -a "命令" -b -i inventory.txt`

**说明**：`-i` 指定主机清单，`-b` 表示提升权限（become）。

</div>

<div class="kb-card" markdown="1">

## Ansible playbook 基本结构

*未标注* <span class="kb-pill">#ansible</span> <span class="kb-pill">#playbook</span>

> playbook 是 Ansible 的剧本文件，按顺序执行 tasks，让远端主机达到预期状态。

**主要组成**

- `tasks`：要执行的任务列表
- `variables`：变量，可使用 facts、用户自定义变量或 roles 传递
- `templates`：使用 Jinja2 模板渲染配置文件
- 条件判断与字典：根据变量控制任务执行
- `roles`：把相关的任务、模板、变量打包复用

</div>
