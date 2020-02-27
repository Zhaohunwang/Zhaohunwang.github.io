---
title: sqlserver取随机数据
date: 2020-02-27 13:51:19
tags: sql
---

在sqlserver中查询随机排列的数据

```sql
SELECT  * FROM Db ORDER BY NEWID()

```

newid()的返回值 是uniqueidentifier ,order by newid()随机选取记录是如何进行的 newid()在扫描每条记录的时候都生成一个值, 而生成的值是随机的, 没有大小写顺序. 所以最终结果再按这个排序, 排序的结果当然就是无序的了

参考资料

[NEWID (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/functions/newid-transact-sql?view=sql-server-2017)

