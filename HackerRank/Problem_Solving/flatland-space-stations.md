# 思路
模拟题, 注意空间站数组不一定是顺序排列的

# 算法复杂度

O(n)

# python3 代码

```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the flatlandSpaceStations function below.
def flatlandSpaceStations(n, c):
    c.sort()    # c不一定是顺序排列
    dist = []
    nearest = 0
    for i in range(n):
        if c[nearest] < i:
            nearest = min(nearest+1, len(c)-1)

        d = min(abs(c[max(nearest-1, 0)] - i), abs(c[nearest] - i))
        dist.append(d)

    return max(dist)

        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nm = input().split()

    n = int(nm[0])

    m = int(nm[1])

    c = list(map(int, input().rstrip().split()))

    result = flatlandSpaceStations(n, c)

    fptr.write(str(result) + '\n')

    fptr.close()

```