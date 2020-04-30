#### 查询跑批工单解压密码

```sql
select  t1.product_id,t1.var from DSP.DS_ORDER_PRODUCT t1 where t1.ORDER_ID in('LOG0000000129577','LOG0000000129578') 
```



#### 查询实验室密码

```sql
select t1.MODELING_ID,t2.CODE_NAME,t1.ZIPPASSWORD from DSP.DS_MODELING_PRODUCT_COUNT t1 ,DSP.DS_CODE t2 where t2.CODE_CODE = t1.PRODUCT_CODE and t2.CODE_TYPE_ID in (select id from DSP.DS_CODETYPE where CODETYPE_CODE='variableTypeCode') and t1.MODELING_ID in('lab0129796')
```



#### 业务层重载

```shell
/home/hadoop/application_batch/Dps-operation-service-bs3_Restructure_9017/resource
```



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



