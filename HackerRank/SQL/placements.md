# 类型

多表连接, 子查询

# 难度

中

# 思路

我觉得这题比较难的地方是排序。  
开始的时候用select from in (子查询), 发现结果是错了，后来才发现in中的顺序和子查询出来的顺序不一样，原来被打乱了（或是重新排序了）。  

# MySQL代码

```
select 
    (select Name from Students where ID = f.id) `Name`
from 
    Friends f inner join Packages p1 on f.ID = p1.ID
    inner join Packages p2 on f.Friend_ID = p2.ID
    where p1.Salary < p2.Salary
    order by p2.Salary
```