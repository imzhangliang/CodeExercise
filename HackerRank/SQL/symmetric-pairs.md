# 类型

子查询，条件查询

# 难度

中

# 思路

分两种情况：  
1. x和y不同  
2. x和y相同  
  
然后再用distinct去重


# MySQL代码

```
select distinct
    f1.*
from Functions f1
where (f1.x < f1.y and exists(select * from Functions where x = f1.y and y = f1.x))
or (f1.x = f1.y and (select count(*) from Functions where x = f1.x and y = f1.x) >= 2)
order by f1.x, f1.y
```