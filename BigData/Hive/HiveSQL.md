# Hive SQL 练习

## 查询累积销量排名第二的商品

> 查询订单明细表（order_detail）中销量（下单件数）排名第二的商品id，如果不存在返回null，如果存在多个排名第二的商品则需要全部返回。

- 总结、沉淀：

  - 如果不存在返回null，用到了`right join`

    ```sql
    # null_table 一个空表
    select id
    from null_table
    right join (
        select 1
    ) t1
    on 1 = 1;
    ```

  - rank()、dense_rank()、row_number()

- 代码

```sql
select sku_id
from (
         select sku_id
         from (
                  select sku_id,
                         order_num,
                         dense_rank() over (order by order_num desc) rk
                  from (
                           select sku_id,
                                  sum(sku_num) order_num
                           from order_detail
                           group by sku_id
                       ) t1
              ) t2
         where rk = 2
     ) t3
         right join --为保证，没有第二名的情况下，返回null
     (
         select 1
     ) t4
     on 1 = 1; 
```





## 查询至少连续三天下单的用户

> 查询订单信息表(order_info)中最少连续3天下单的用户id，

- 总结、沉淀：

  - 判断一串日期是否连续：若连续，用这个日期减去它的排名，会得到一个相同的结果

  

- 代码：

  ```sql
  select distinct user_id
  from (
           select user_id
           from (
                    select user_id,
               			 create_date,
                           date_sub(create_date, row_number() over (partition by user_id order by create_date)) flag
                    from (
                             select user_id,
                                    create_date
                             from order_info
                             group by user_id, create_date
                         ) t1 -- 同一天可能多个用户下单，进行去重
                ) t2 -- 判断一串日期是否连续：若连续，用这个日期减去它的排名，会得到一个相同的结果
           group by user_id, flag
           having count(flag) >= 3 -- 连续下单大于等于三天
       ) t3;
  ```

  



## 查询各品类销售商品的种类数及销量最高的商品

> 从订单明细表(order_detail)统计各品类销售出的商品种类数及累积销量最好的商品

















| 数据类型 | 描述                                                         | 语法示例                                          |
| -------- | ------------------------------------------------------------ | ------------------------------------------------- |
| STRUCT   | 和 c 语言中的 struct 类似，都可以通过“点”符号访 问元素内容。例如，如果某个列的数据类型是 STRUCT{first STRING, last STRING},那么第 1 个元素可以通过字段.first 来 引用。 | struct() 例 如 struct<street:string, city:string> |
| MAP      | MAP 是一组键-值对元组集合，使用数组表示法可以 访问数据。例如，如果某个列的数据类型是 MAP，其中键 ->值对是’ first’ ->’ John’和’ last’ ->’ Doe’，那么可以 通过字段名[‘last’ ]获取最后一个元素 | map() 例如 map<string, int>                       |
| ARRAY    | 数组是一组具有相同类型和名称的变量的集合。这些 变量称为数组的元素，每个数组元素都有一个编号，编号从 零开始。例如，数组值为[‘John’ , ‘Doe’ ]，那么第 2 个 元素可以通过数组名[1]进行引用。 | Array() 例如 array<string>                        |

















