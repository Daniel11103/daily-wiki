# vscode

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 用正则批量替换日期格式

*2024-01-15* · <span class="kb-pill">#vscode</span> <span class="kb-pill">#正则</span>

> 把 `[10_02_22_45]` 批量改为 `[10-02_22-45]`。

**步骤**

1. `Ctrl+F`（Mac：`Cmd+F`）打开查找，点击 `.*` 开启正则
2. 查找：`\[(\d{2})_(\d{2})_(\d{2})_(\d{2})\]`
3. 替换：`[$1-$2_$3-$4]`
4. 点击「全部替换」

**注意**：一次性操作，之后再用需重新执行。

</div>
