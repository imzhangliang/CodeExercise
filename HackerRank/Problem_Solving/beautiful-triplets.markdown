

# 思路

开始的时候用暴搜或暴搜+剪枝都超时，最后想了一下其实这个题考的无非是所有  
&nbsp;&nbsp;&nbsp;&nbsp;*i的个数 * (i+d)的个数 * (i+2*d)的个数*  
情况的总和。  
那么用表存即可。  

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

# Complete the beautifulTriplets function below.
def beautifulTriplets(d, arr):
    n = len(arr)
    count = 0

    indexes = [0 for i in range(20010)]
    for i in range(n):
        indexes[arr[i]] += 1


    for i in range(20010 - 2*d):
        count += indexes[i] * indexes[i+d] * indexes[i+2*d]


    return count


if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nd = input().split()

    n = int(nd[0])

    d = int(nd[1])

    arr = list(map(int, input().rstrip().split()))

    result = beautifulTriplets(d, arr)

    fptr.write(str(result) + '\n')

    fptr.close()


```

# 解法2
从discussion上面看到了一个更加简洁的方法.如果python的in用的是索引，也会很高效率。

```
def beautifulTriplets(d, arr):
    count = 0

    for item in arr:
        if item+d in arr and item+d*2 in arr:
            count += 1


    return count
```