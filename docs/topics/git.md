# git

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 重命名 Git 分支

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#分支</span>

> 本地分支直接改名即可；已推送的远程分支需要删除旧分支并重新推送。

**步骤**

1. 本地改名：`git branch -m <旧名> <新名>`
2. 删除远程旧分支：`git push --delete origin <旧名>`
3. 推送新分支：`git push origin <新名>`
4. 重新关联远程：`git branch --set-upstream-to origin/<新名>`

</div>

<div class="kb-card" markdown="1">

## 把修改从错误的分支转移到正确分支

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#分支</span>

> 在错误分支上修改代码后，可用 stash 把修改转移到正确的分支。

**步骤**

1. `git stash` 暂存当前修改
2. `git checkout <正确分支>` 切换分支
3. `git stash pop` 应用修改，有冲突时手动解决

**注意**：前提是还没有执行 `git add`。

</div>

<div class="kb-card" markdown="1">

## GitLab Flow 分支管理规范

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#规范</span>

> 用 master 发布、develop 开发，功能和补丁分支完成后合并并删除。

**分支说明**

- `master`：稳定的发布版本，每次发布打 Tag
- `develop`：日常开发和功能测试
- `feat-xxx`：功能分支，从 develop 切出，完成后合并回 develop
- `fix-xxx`：测试环境补丁，从 develop 切出
- `hotfix-xxx`：正式环境补丁，从 master 切出，完成后合并回 master 和 develop

**注意**：master 通常设置分支保护，合并需提交合并申请，由项目管理员处理。

</div>

<div class="kb-card" markdown="1">

## 使用约定式提交规范书写 commit message

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#规范</span>

> 按 `<类型>[作用域]: <描述>` 的格式书写提交信息，便于阅读和自动化处理。

**步骤**

1. 全局安装：`npm install -g commitizen cz-conventional-changelog`
2. 配置适配器：`echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc`
3. 用 `git cz` 代替 `git commit` 提交

</div>

<div class="kb-card" markdown="1">

## clone、fetch 与 pull 的区别

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#远程</span>

> `git clone` 克隆整个仓库；`git pull` 等于 `git fetch` 加 `git merge`。

**步骤**

1. `git clone <仓库地址> [本地目录名]`，无需先 `git init`
2. `git fetch` 只获取远程更新，不做合并
3. `git pull <远程> <远程分支>:<本地分支>` 获取并合并到本地

</div>

<div class="kb-card" markdown="1">

## 基于 develop 的功能分支开发流程

*未标注* <span class="kb-pill">#git</span> <span class="kb-pill">#流程</span>

> 从 develop 切出功能分支开发，完成后合并回 develop 并删除功能分支。

**步骤**

1. `git checkout -b feature/<名称> origin/develop` 切出功能分支
2. 开发后执行 `git add` 和 `git commit`
3. `git pull origin develop` 先同步，再 `git checkout develop` 和 `git merge feature/<名称>`，最后 `git push`
4. `git branch -d feature/<名称>` 删除本地功能分支

</div>
