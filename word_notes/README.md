#### 查询跑批工单解压密码

> select  t1.product_id,t1.var from DSP.DS_ORDER_PRODUCT t1 where t1.ORDER_ID in('LOG0000000129577','LOG0000000129578') 



---





#### 业务层重载

> /home/hadoop/application_batch/Dps-operation-service-bs3_Restructure_9017/resource



---



#### 聚合日志地址

> 日志服务器
>
> 10.102.1.58
>
> 前置聚合日志存储路径
>
> /home/hadoop/application/log/Dps-LogConsume/qianzhi
>
> 数据源聚合日志存储路径
>
> /home/hadoop/application/log/Dps-LogConsume/dataSource
>
> 前置实时聚合日志
>
> qianzhi_new_response_arg_simple.{yyyy-MM-dd}.log
>
> 跑批聚合日志
>
> batch_qianzhi_new_response_arg_simple.{yyyy-MM-dd}.log



