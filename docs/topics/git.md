# git

## rebase 冲突处理（样例） (2026-11-12)

标签：#git #冲突

- 先 `git fetch` 获取最新远程分支
- 执行 `git rebase`，出现冲突时编辑冲突文件
- 解决后 `git add <文件>`，再执行 `git rebase --continue`
- 与 [python](python.md) 无关，仅用于测试双链
