# 类型

多表连接, 子查询，聚合操作

# 难度

中

# 思路

解法很妙，看代码就知道了。  
参考了discussions里的答案， 不过我没有用sql_mode = '', 用了min(End_Date).


# Mysql代码

```
SELECT Start_Date, min(End_Date)
FROM 
    (SELECT Start_Date FROM Projects WHERE Start_Date NOT IN (SELECT End_Date FROM Projects)) a,
    (SELECT End_Date FROM Projects WHERE End_Date NOT IN (SELECT Start_Date FROM Projects)) b 
WHERE Start_Date < End_Date
GROUP BY Start_Date 
ORDER BY DATEDIFF(min(End_Date), Start_Date), Start_Date
```