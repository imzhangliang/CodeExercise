# 类型
多表连接

# 难度
中

# 思路
开始很容易想到用group by, 可一旦用group by, 找最小的费用的对应的id就不好弄了。看了下discussion。  
用子查询先查出最小值，然后在用where过滤出来即可。  

# MySQL代码
```
select 
    w.id,
    wp.age,
    w.coins_needed,
    w.power
from Wands w
inner join Wands_Property wp on w.code = wp.code
where 
    wp.is_evil = 0
    and w.coins_needed = (select min(coins_needed) from Wands w2 inner join Wands_Property wp2 on w2.code = wp2.code where w2.power = w.power and wp2.age = wp.age)
    order by w.power desc, wp.age desc
```


