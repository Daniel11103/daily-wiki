# mysql

[全部主题](../index.md){ .md-button }

<div class="kb-card" markdown="1">

## 查询数据库占用空间

*未标注* <span class="kb-pill">#mysql</span> <span class="kb-pill">#运维</span>

> 从 `information_schema` 汇总每个数据库的数据和索引大小。

**步骤**
```sql
SELECT table_schema,
       SUM(data_length + index_length) / 1024 / 1024 AS total_mb,
       SUM(data_length) / 1024 / 1024 AS data_mb,
       SUM(index_length) / 1024 / 1024 AS index_mb
FROM information_schema.tables
GROUP BY table_schema
ORDER BY total_mb DESC;
```

</div>

<div class="kb-card" markdown="1">

## 常用备份与导入命令

*未标注* <span class="kb-pill">#mysql</span> <span class="kb-pill">#备份</span>

> 用 `mysqldump` 导出数据库或表，用 `source` 导入。

**步骤**

1. 导出整个数据库：`mysqldump -u <用户名> -p <数据库名> > 文件.sql`
2. 导出单个表：`mysqldump -u <用户名> -p <数据库名> <表名> > 文件.sql`
3. 只导出结构（不含数据）：`mysqldump -u <用户名> -p -d <数据库名> > 结构.sql`
4. 导入：登录 mysql 后执行 `source 文件.sql`

**注意**：命令中的密码不要直接写在命令行里，使用 `-p` 交互式输入。

</div>
