# 思路
简单模拟题。   
但要注意字符串和数字类型的转化问题。  
如果用python，字符串中的字符不能直接赋值。

# 算法复杂度

O(n^2)

# python3 代码

```
#!/bin/python3

import math
import os
import random
import re
import sys

def isHole(grid, i, j):
    if int(grid[i][j]) > int(grid[i][j-1]) and int(grid[i][j]) > int(grid[i][j+1]) and int(grid[i][j]) > int(grid[i-1][j]) and int(grid[i][j]) > int(grid[i+1][j]):
        return True
    else:
        return False

# Complete the cavityMap function below.
def cavityMap(grid):
    n = len(grid)

    flag = [[0 for j in range(n)] for i in range(n)]

    for i in range(1, n-1):
        for j in range(1, n-1):
            if isHole(grid, i, j):
                flag[i][j] = 1

    for i in range(1, n-1):
        for j in range(1, n-1):
            if flag[i][j]:
                grid[i] = grid[i][:j] + 'X' + grid[i][j+1:]

    return grid


if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    grid = []

    for _ in range(n):
        grid_item = input()
        grid.append(grid_item)

    result = cavityMap(grid)

    fptr.write('\n'.join(result))
    fptr.write('\n')

    fptr.close()


```
