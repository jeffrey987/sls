# RDS安全

本文介绍RDS安全的告警规则。通过设置告警规则，可及时触发告警，有助于您快速发现RDS安全问题。

## 告警规则列表

支持的告警规则列表如下所示。设置告警参数、设置白名单等相关操作，请参见[管理告警规则](/intl.zh-CN/应用中心（App）/日志审计服务/告警/管理告警规则.md)。

-   [RDS慢SQL检测](#section_j3n_8le_9ze)
-   [RDS大批量数据删除告警](#section_dpl_pgt_f9q)
-   [RDS外网访问检测](#section_qbg_bpr_mw1)
-   [RDS查询SQL平均执行时间监控告警](#section_r6k_k0m_s6t)
-   [RDS数据库更新峰值监控告警](#section_g7s_gyy_cjq)
-   [RDS数据库查询峰值监控告警](#section_wn6_l4j_bar)
-   [RDS实例释放告警](#section_924_ayp_1qs)
-   [RDS高频访问IP检测](#section_e6x_s3n_vvu)
-   [RDS更新SQL平均执行时间监控告警](#section_jwx_h6s_9fl)
-   [RDS登录失败次数过多告警](#section_0j0_ema_u8m)
-   [RDS大批量数据修改事件告警](#section_fm1_jd3_da6)
-   [RDS危险的SQL执行告警](#section_5ej_zg6_xno)
-   [RDS SQL执行错误数过多告警](#section_j7h_vch_u4y)

## RDS慢SQL检测

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_slow\_sql|
|**告警名称**|RDS慢SQL检测|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS SQL执行是否为慢SQL。RDS SQL执行时间大于等于规则参数慢SQL时间阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS慢SQL检测。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   慢SQL时间阈值：SQL执行时间大于该阈值时，判定为慢SQL。默认值为5000微妙。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控阿里云账号下的所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控阿里云账号下的所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查出现慢SQL的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS大批量数据删除告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_batch\_del\_sql|
|**告警名称**|RDS大批量数据删除告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS是否大量删除数据。删除的RDS数据行数大于等于规则参数大批量删除界定阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS大批量数据删除告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   大批量删除界定阈值：删除数据行数的最大值。默认值为10。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控阿里云账号下的所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控阿里云账号下的所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查发生大批量删除事件的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS外网访问检测

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_internet\_access|
|**告警名称**|RDS外网访问检测|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS是否被外网IP地址访问。RDS被外网IP地址访问时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|严重度：严重、高、中、低、报告。默认值为高。|
|**外部配置**|允许通过外网访问的RDS实例白名单。白名单中的RDS实例被外网IP地址访问时，不会触发告警。|
|**消除方法**|禁止白名单以外的RDS实例被外网IP地址访问。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS查询SQL平均执行时间监控告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_select\_speed|
|**告警名称**|RDS查询SQL平均执行时间监控告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS每条查询SQL执行平均时间。RDS SQL查询语句平均执行时间大于等于规则参数SQL平均执行时间阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS查询SQL平均执行时间监控告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   SQL平均执行时间阈值：查询语句SQL平均执行时间的最大值。默认值为0.005秒/条。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控该阿里云账号下的所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查查询SQL的平均执行时间过长的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS数据库更新峰值监控告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_update\_peak|
|**告警名称**|RDS数据库更新峰值监控告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS更新（增删改）峰值。RDS更新（增删改）峰值大于等于规则参数更新峰值阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS数据库更新峰值监控告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   更新峰值阈值：RDS更新（增删改）峰值。默认值为100行/秒。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查更新峰值过高的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS数据库查询峰值监控告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_query\_peak|
|**告警名称**|RDS数据库查询峰值监控告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS查询峰值。RDS查询峰值大于等于规则参数查询峰值阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS数据库查询峰值监控告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   查询峰值阈值：RDS查询峰值。默认值为1000行/秒。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查查询峰值过高的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS实例释放告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_instance\_del|
|**告警名称**|RDS实例释放告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS实例释放异常。RDS实例被释放时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|严重度：严重、高、中、低、报告。默认值为高。|
|**外部配置**|无|
|**消除方法**|检查被释放的RDS实例是否属于正常释放。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS高频访问IP检测

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_visit|
|**告警名称**|RDS高频访问IP检测|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控同一个IP地址对RDS实例访问频率是否异常。同一个IP地址对RDS实例访问频率大于等于规则参数高频访问阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS高频访问IP检测。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   高频访问阈值：每2分钟内，同一个IP地址对一个RDS实例的访问次数最大值。默认值为30次。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。 |
|**外部配置**|RDS高频访问IP地址白名单。白名单中的IP地址对RDS实例发起高频访问时，不会触发告警。|
|**消除方法**|检查高频访问RDS实例的IP地址是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS更新SQL平均执行时间监控告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_update\_speed|
|**告警名称**|RDS更新SQL平均执行时间监控告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS每条更新（增删改）SQL执行平均时间。RDS更新（增删改）SQL平均执行时间大于等于规则参数SQL平均执行时间阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS更新SQL平均执行时间监控告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   SQL平均执行时间阈值：更新（增删改）SQL平均执行时间的最大值。默认值为0.005秒/条。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查更新（增删改）SQL的平均执行时间过长的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS登录失败次数过多告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_login\_err\_cnt|
|**告警名称**|RDS登录失败次数过多告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控登录RDS实例失败次数是否异常。一个RDS实例在5分钟内登录失败次数大于等于规则参数最大失败登录次数时，会触发告警。|
|**执行频率**|固定时间间隔：4分钟|
|**查询范围**|过去5分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS登录失败次数过多告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   最大失败登录次数：一个RDS实例5分钟内允许登录失败次数的最大值。默认值为3次。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。 |
|**外部配置**|无|
|**消除方法**|检查登录失败次数过的RDS实例是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS大批量数据修改事件告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_batch\_update\_sql|
|**告警名称**|RDS大批量数据修改事件告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS大量修改数据是否异常。RDS大量修改数据行数大于等于规则参数大规模修改界定阈值时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS大批量数据修改事件告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   大规模修改界定阈值：修改数据行数的最大值。默认值为10。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查发生大批量数据修改事件的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS危险的SQL执行告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_danger\_sql|
|**告警名称**|RDS危险的SQL执行告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS是否存在执行危险SQL。RDS出现执行危险SQL时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS危险的SQL执行告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查执行危险SQL的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

## RDS SQL执行错误数过多告警

|**告警ID**|sls\_app\_audit\_db\_at\_rds\_sql\_err\_cnt|
|**告警名称**|RDS SQL执行错误数过多告警|
|**版本号**|1|
|**类别**|云平台、阿里云、数据库安全、RDS安全|
|**作用**|监控RDS SQL执行错误次数是否异常。一个RDS实例的SQL执行错误次数大于等于规则参数最大错误次数时，会触发告警。|
|**执行频率**|固定时间间隔：1分钟|
|**查询范围**|过去2分钟|
|**参数配置**|-   告警名称：告警实例的名称，默认为RDS SQL执行错误数过多告警。您可以根据不同监控对象，命名不同的告警名称便于识别。
-   严重度：严重、高、中、低、报告。默认值为高。
-   最大错误次数：一个RDS实例2分钟内允许SQL执行错误的最大次数。默认值为10。
-   阿里云账号ID：需要监控的阿里云账号ID（支持正则）。
    -   多个阿里云账号ID之间可以使用竖线（\|）分隔。您还可以使用正则表达式`.*`进行配置，例如156133.\*，表示监控以156133开头的阿里云账号。
    -   默认值为`.*`，表示监控审计服务下配置的所有阿里云账号。
-   RDS实例ID：待监控的RDS实例ID（支持正则表达式）。默认值`.*`，表示监控所有RDS实例。
-   数据库名称：待监控的数据库名称（支持正则表达式）。默认值`.*`，表示监控所有数据库。 |
|**外部配置**|无|
|**消除方法**|检查SQL执行错误次数过多的RDS数据库是否存在异常。|
|**前提条件**|确保已在日志审计服务中的**审计配置** \> **云产品接入** \> **全局配置**中打开RDS **SQL审计日志**的开关。|

