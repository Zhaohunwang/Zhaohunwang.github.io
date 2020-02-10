---
title: sqlserver下查询前一条数据
date: 2020-02-10 17:46:58
tags: sql
---
查询某条数据的前一条数据以及后一条数据，例如 上一篇文章、下一篇文章

```sql
with TB as (
select *,row_number() over(order by a_order desc,id desc) as rowid from Table order by a_order desc,id desc)
--上一条：
select * from TB where rowid=(select rowid-1 from TB where id=6)

```

c#下代码如下

```c#
using (var connection = new SqlConnection(_connectionString))
            {
                var sql =
                    $@"SELECT p.rowid from (
                  SELECT ROW_NUMBER() OVER (ORDER BY CreateTime desc) AS rowid,Id,CreateTime  FROM dbo.Articles 
                  ) AS p WHERE p.Id ='{id.ToString()}'";
                var rowId = await connection.QueryFirstOrDefaultAsync<int>(sql);
                if (rowId > 0)
                {
                    var sqlQuery = $@"
                SELECT * FROM (
                    SELECT ROW_NUMBER() OVER (ORDER BY CreateTime desc) AS rowid,*  FROM dbo.Articles
	                ) AS p WHERE p.rowid >=  {rowId-1} AND p.rowid<={rowId+1} ";
                    var result = await connection.QueryAsync<Article>(sqlQuery);
                    return result;
                }
                else
                {
                    return null;
                }
            }
```

