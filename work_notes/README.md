#### 配置

> 10.102.1.58

```shell
db2 connect to dcp54 user etl using etl
```

```sql
SELECT T1.* FROM DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 WHERE T1.PROTOCOL_ID in ('P0128066','P0001452','P0001444')

update  DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 set t1.ISVALID=0  WHERE T1.PROTOCOL_ID in ('P0001224','P0001430','P0127581','P0127586','P0127587','P0127682','P0127686')
-- 商户
select t1.MER_CODE,t1.MER_NAME from dsp.DS_MERCHANT t1 where t1.ID in (1181624,109481,1730510,1229946,1298221,1693559)
-- 产品
select t1.PRODUCT_SUITES_CODE from dsp.DS_PRODUCT_SUITES t1 where t1.ID in (1880948,1731954,1907671,1908369,1915392,1304131,1731949,1945301,14368,1200821)

select t1.*  from DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 where t1.PROTOCOL_ID in (select DISTINCT t1.PROTOCOL_ID from   DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 WHERE t1.PROTOCOL_ID not IN (select DISTINCT T2.PROTOCOL_ID from DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 INNER JOIN dsp.DS_MERCHANT_SIGN_PRODUCT_SUITES_SUPPLEMENT t2 ON t1.PROTOCOL_ID = t2.PROTOCOL_ID) and t1.ISMASTER=1 and t1.PROTOCOL_ID !='P000TEST' and t1.ISVALID=1)



select DISTINCT T2.PROTOCOL_ID from DSP.DS_MERCHANT_SIGN_PRODUCT_SUITES T1 INNER JOIN dsp.DS_MERCHANT_SIGN_PRODUCT_SUITES_SUPPLEMENT t2 ON t1.PROTOCOL_ID = t2.PROTOCOL_ID WHERE t1.PROTOCOL_ID in  ('P0128066','P0001452','P0001444') ;

```



#### 查看DB2数据库表结构

```sql
SELECT T1.TABSCHEMA,T1.TABNAME,T1.COLNAME,T1.COLNO,T1.TYPENAME,T1.LENGTH,T1.REMARKS,T1.NULLS,T1.KEYSEQ FROM SYSCAT.COLUMNS T1 WHERE T1.TABNAME='DS_SIGN_DOCUMENT' AND T1.TABSCHEMA='DSP'
```



#### 添加数据库字段

```sql
ALTER TABLE DSP.DS_ORDER ADD COLUMN MERCHANT_CONTACT VARCHAR(100) NOT NULL DEFAULT '';
ALTER TABLE DSP.DS_ORDER ADD COLUMN RESULT_EMAIL VARCHAR(100) NOT NULL DEFAULT '';
ALTER TABLE DSP.DS_ORDER ADD COLUMN RESULT_TYPE SMALLINT NOT NULL DEFAULT 1;
COMMENT ON COLUMN DSP.DS_ORDER.MERCHANT_CONTACT IS '商户联系人';
COMMENT ON COLUMN DSP.DS_ORDER.RESULT_EMAIL IS '结果返回邮箱';
COMMENT ON COLUMN DSP.DS_ORDER.RESULT_TYPE IS '结果返回类型';
```



#### 查询跑批工单解压密码

```sql
select  t1.order_id,t1.product_id,t1.var from DSP.DS_ORDER_PRODUCT t1 where t1.ORDER_ID in('LOG0000000129577')
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



#### 新版runningCool错误码

| 错误码 | 描述                         |
| ------ | ---------------------------- |
| 0000   | 处理成功                     |
| 0101   | 限免条数样本，不参与请求前置 |
| 0102   | 样本校验未通过，不参与请求   |
| 0103   | 样本解析异常                 |
| 7777   | 限免条数样本，不参与请求前置 |
| 8888   | 样本校验未通过，不参与请求   |
| 9998   | 样本解析异常                 |
| 9999   | 请求跑批前置异常             |

