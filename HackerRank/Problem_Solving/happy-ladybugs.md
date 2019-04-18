# 思路

可以发现当存在 _ 字符时，任意两个字符之间，是可以借助一个_进行交换的, 那么就是说只要存在_字符，就可以实现先有字符的所有排列。  
题解分两种情况：  
1. 不存在_字符时  
此时不能做任何交换，只需判断每个ladybug是否happy  
2. 存在_字符时  
此时可以实现任意排列，只需判断是否有单个颜色的ladybug  

# 算法复杂度: 
O(n)


# python3代码
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the happyLadybugs function below.
def happyLadybugs(b):
    happy = True
    if '_' not in b:        # 没有_字符的情况，那么是不能移动的，只需判断是否有不开心的ladybug
        n = len(b)
        b = '*' + b + '*'   # 加2个边界哨兵
        for i in range(1, n+1):
            if b[i-1] != b[i] and b[i] != b[i+1]:
                happy = False
                break
    else:                   # 有_的情况，任何两个字符都可以替换，可以变成任意排列. 只需统计是否存在单个字符的情况
        charDict = {}
        for c in b:
            if c != '_':
                if c not in charDict:
                    charDict[c] = 1
                else:
                    charDict[c] += 1

        for c in charDict:
            if charDict[c] == 1:
                happy = False
                break

    return 'YES' if happy else 'NO'



if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    g = int(input())

    for g_itr in range(g):
        n = int(input())

        b = input()

        result = happyLadybugs(b)

        fptr.write(result + '\n')

    fptr.close()

```