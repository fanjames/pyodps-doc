常见问题
========

**读取数据时报"project is protected"**

Project
上的安全策略禁止读取表中的数据，此时，如果想使用全部数据，有以下选项可用：

-   联系 Project Owner 增加例外规则
-   使用 DataWorks 或其他脱敏工具先对数据进行脱敏，导出到非保护
    Project，再进行读取

如果只想查看部分数据，有以下选项

-   改用 `o.execute_sql('select * from <table_name>').open_reader()`
-   改用 DataFrame &lt;df&gt;，`o.get_table('<table_name>').to_df()`

**出现 ImportError，并且在 ipython 或者 jupyter 下使用**

如果 `from odps import errors` 也不行，则是缺少 ipython 组件，执行
`pip install -U jupyter` 解决。

**执行 SQL 通过 open\_reader 只能取到最多1万条记录，如何取多余1万条？**

使用 `create table as select ...` 把SQL的结果保存成表，再使用
table.open\_reader &lt;table\_open\_reader&gt; 来读取。

**上传 pandas DataFrame 到 ODPS 时报错：ODPSError: ODPS entrance should
be provided**

原因是没有找到全局的ODPS入口，有三个方法：

-   使用 room 机制 &lt;cl&gt; ，`%enter` 的时候，会配置全局入口
-   对odps入口调用 `to_global` 方法
-   使用odps参数，`DataFrame(pd_df).persist('your_table', odps=odps)`

**在 DataFrame 中如何使用 max\_pt ？**

使用 `odps.df.func` 模块来调用 ODPS 内建函数

``` {.sourceCode .python}
from odps.df import func
df = o.get_table('your_table').to_df()
df[df.ds == func.max_pt('your_project.your_table')]  # ds 是分区字段
```

**通过 DataFrame 写表时报 table lifecycle is not specified in mandatory
mode**

Project 要求对每张表设置 lifecycle，因而需要在每次执行时设置

``` {.sourceCode .python}
from odps import options
options.lifecycle = 7  # 或者你期望的 lifecycle 整数值，单位为天
```
