# 类型

多表连接, 聚合操作

# 难度

中

# 思路

不多说，看代码。  
主要是第2钟情况having钟不能用hacker_count, 只能用这样一种看起来低效的方法。


# MySQL代码
```
select 
    ha.hacker_id,
    ha.name,
    count(ch.challenge_id) hacker_count
from Hackers ha inner join Challenges ch on ha.hacker_id = ch.hacker_id
group by ha.hacker_id,ha.name
having 
-- 第一种情况：创建的题目刚好是最大数
hacker_count = (select max(t1.cnt) from 
                  (select hacker_id, count(*) as cnt from Challenges group by hacker_id) t1)
                  
-- 第2中情况：创建的题目数是唯一的
 or hacker_count in
 (select t1.cnt from 
                   (select hacker_id, count(*) as cnt from Challenges group by hacker_id) t1
        group by t1.cnt having count(*) = 1
 )

order by hacker_count desc, ha.hacker_id
```