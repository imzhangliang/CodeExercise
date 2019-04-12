# 思路
挺有意思的一道模拟题

# 算法复杂度

O(logn)

# python3 代码

```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the chocolateFeast function below.
def chocolateFeast(n, c, m):
    bars = n//c
    wrappers = n//c

    while wrappers >= m:
        bars += wrappers//m
        wrappers = wrappers%m + wrappers//m

    return bars

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    for t_itr in range(t):
        ncm = input().split()

        n = int(ncm[0])

        c = int(ncm[1])

        m = int(ncm[2])

        result = chocolateFeast(n, c, m)

        fptr.write(str(result) + '\n')

    fptr.close()

```
