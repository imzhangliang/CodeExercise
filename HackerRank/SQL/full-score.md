# 类型

联表查询，聚合查询

# 难度

中

# 思路

注：Challenges表中的hacker_id是创建者的id，本查询用不上  
查询的步骤如下：
1. 先找出所有满分的提交并去重  
2. 再从满分提交中获得多于1满分提交的人
3. 按题意排序


# MySQL代码

```
select
ha.hacker_id, ha.name
from Hackers ha
inner join
(select distinct
    sub.hacker_id, sub.challenge_id
from Submissions sub inner join Challenges ch on sub.challenge_id = ch.challenge_id
inner join Difficulty diff on ch.difficulty_level = diff.difficulty_level
where sub.score = diff.score) t1 on ha.hacker_id = t1.hacker_id
group by ha.hacker_id, ha.name
having count(*) > 1
order by count(*) desc, ha.hacker_id
```