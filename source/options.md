配置选项
========

PyODPS 提供了一系列的配置选项，可通过 `odps.options`
获得，如下面的例子：

``` {.sourceCode .python}
from odps import options
# 设置所有输出表的生命周期（lifecycle 选项）
options.lifecycle = 30
# 使用 Tunnel 下载 string 类型时使用 bytes（tunnel.string_as_binary 选项）
options.tunnel.string_as_binary = True
# PyODPS DataFrame 用 ODPS 执行时，参照下面 dataframe 相关配置，sort 时设置 limit 到一个比较大的值
options.df.odps.sort.limit = 100000000
```

下面列出了可配的 ODPS 选项。

通用配置
--------

  选项                                                                                 说明                                                                                                                                                                            默认值
  ------------------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------
  end\_point                                                                           ODPS Endpoint                                                                                                                                                                   None
  default\_project                                                                     默认 Project                                                                                                                                                                    None
  log\_view\_host                                                                      LogView 主机名                                                                                                                                                                  None
  log\_view\_hours                                                                     LogView 保持时间（小时）                                                                                                                                                        24
  local\_timezone                                                                      使用的时区，True 表示本地时间，False 表示 UTC， 也可用 pytz 的时区                                                                                                              1
  lifecycle                                                                            所有表生命周期                                                                                                                                                                  None
  temp\_lifecycle                                                                      临时表生命周期                                                                                                                                                                  1
  biz\_id                                                                              用户 ID                                                                                                                                                                         None
  verbose                                                                              是否打印日志                                                                                                                                                                    False
  verbose\_log                                                                         日志接收器                                                                                                                                                                      None
  chunk\_size                                                                          写入缓冲区大小                                                                                                                                                                  1496
  retry\_times                                                                         请求重试次数                                                                                                                                                                    4
  pool\_connections                                                                    缓存在连接池的连接数                                                                                                                                                            10
  pool\_maxsize                                                                        连接池最大容量                                                                                                                                                                  10
  connect\_timeout                                                                     连接超时                                                                                                                                                                        5
  read\_timeout                                                                        读取超时                                                                                                                                                                        120
  api\_proxy                                                                           API 代理服务器                                                                                                                                                                  None
  data\_proxy                                                                          数据代理服务器                                                                                                                                                                  None
  completion\_size                                                                     对象补全列举条数限制                                                                                                                                                            10
  notebook\_repr\_widget                                                               使用交互式图表                                                                                                                                                                  True
  sql.settings                                                                         ODPS SQL运行全局hints                                                                                                                                                           None
  sql.use\_odps2\_extension                                                            启用 MaxCompute 2.0 语言扩展                                                                                                                                                    False

数据上传/下载配置
-----------------

  选项 说明                        默认值                                          
  -------------------------------- ----------------------------------------------- ------
  tunnel.endpoint                  Tunnel Endpoint                                 None
  tunnel.use\_instance\_tunnel     使用 Instance Tunnel 获取执行结果 True          
  tunnel.limit\_instance\_tunnel   是否限制 Instance Tunnel 获取结果的条数 None    
  tunnel.string\_as\_binary        在 string 类型中使用 bytes 而非 unicode False   

DataFrame 配置
--------------

  选项 说明                 默认值                                             
  ------------------------- -------------------------------------------------- --
  interactive               是否在交互式环境 根据检测值                        
  df.analyze                是否启用非 ODPS 内置函数 True                      
  df.optimize               是否开启DataFrame全部优化 True                     
  df.optimizes.pp           是否开启DataFrame谓词下推优化 True                 
  df.optimizes.cp           是否开启DataFrame列剪裁优化 True                   
  df.optimizes.tunnel       是否开启DataFrame使用tunnel优化执行 True           
  df.quote                  ODPS SQL后端是否用\`\`来标记字段和表名 True        
  df.libraries              DataFrame运行使用的第三方库（资源名） None         
  df.supersede\_libraries   使用自行上传的numpy替换服务中的版本 False          
  df.odps.sort.limit        DataFrame有排序操作时，默认添加的limit条数 10000   

机器学习配置
------------

  选项 说                   明 默认值                                             
  ------------------------- ----------------------------------------------------- ----------
  ml.xflow\_settings        Xflow 执行配置 Non                                    e
  ml.xflow\_project         默认 Xflow 工程名 algo                                \_public
  ml.use\_model\_transfer   是否使用 ModelTransfer 获取模型 PMML False            
  ml.model\_volume          在使用 ModelTransfer 时使用的 Volume 名称 pyodps\_v   olume


