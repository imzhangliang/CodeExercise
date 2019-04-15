# 思路
动态规划。

a(n) 代表第n个人拥有的面包数  
f(n, 0)代表前n个人的最优解  
f(n, 1)代表第n个人的面包加1时前n个人的最优解  
  
  
推导关系式：  
f(n, 0) = f(n-1, 0)         当 a(n) % 2 = 0
f(n, 0) = f(n-1, 1) + 2     当 a(n) % 2 = 1
  
f(n, 1) = f(n-1, 1) + 2     当 a(n) % 2 = 0
f(n, 1) = f(n-1, 0)         当 a(n) % 2 = 1
  
初始值(以1为起点）：  
当 a(1) % 2 = 0时， f(1,0) = 0, f(1,1) = IMPOSSIBLE  
当 a(1) % 2 = 1时， f(1,0) = IMPOSSIBLE, f(1,1) = 0  

# 思路2 
看了discussions后，貌似也可以用贪心算法，从第1个数向后遍历，遇到奇数时，当前数和后面的数都加1，如果没有遇到n+1位数要加1，那么有解。
  

# 算法复杂度

两种解法都是O(n)

# python3 代码

## 动态规划解法

```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the fairRations function below.
def fairRations(B):
    n = len(B)
    f = [[0,0] for i in range(n)]

    if B[0] % 2 == 0:
        f[0] = [0, -1]
    else:
        f[0] = [-1, 0]

    for i in range(1, n):
        if B[i] % 2 == 0:
            f[i] = [f[i-1][0], f[i-1][1] + 2 if f[i-1][1] >= 0 else -1]
        else:
            f[i] = [f[i-1][1] + 2 if f[i-1][1] >= 0 else -1, f[i-1][0]]

    return f[n-1][0] if f[n-1][0] >= 0 else 'NO'

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    N = int(input())

    B = list(map(int, input().rstrip().split()))

    result = fairRations(B)

    fptr.write(str(result) + '\n')

    fptr.close()

```

## 贪心解法
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the fairRations function below.
def fairRations(B):
    n = len(B)
    B += [0]

    count = 0
    for i in range(n):
        if B[i] % 2 == 1:
            B[i] += 1
            B[i+1] += 1
            count += 2

    if B[n] == 1:
        return 'NO'
    else:
        return count

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    N = int(input())

    B = list(map(int, input().rstrip().split()))

    result = fairRations(B)

    fptr.write(str(result) + '\n')

    fptr.close()

```