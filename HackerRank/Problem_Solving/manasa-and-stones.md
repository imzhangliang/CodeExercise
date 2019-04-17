# 思路1

广度搜索 + 每一层结果哈希去重

# 思路2
所有可能性： a*i + b*(n-1-i),    0 <= i <= n -1  
然后再去重即可


# 算法复杂度: 
思路1: O(2^n)  
思路2: O(n)


# python3代码
思路1

```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the stones function below.
def stones(n, a, b):
    result = {0:1}

    for i in range(1, n):
        tmpResult = {}
        for item in result:
            tmpResult[item + a] = 1
            tmpResult[item + b] = 1

        result = tmpResult

    return sorted(result.keys()) # 注意结果是要升序的

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    T = int(input())

    for T_itr in range(T):
        n = int(input())

        a = int(input())

        b = int(input())

        result = stones(n, a, b)

        fptr.write(' '.join(map(str, result)))
        fptr.write('\n')

    fptr.close()

```

思路2
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the stones function below.
def stones(n, a, b):
    result = []
    if a < b:
        a, b = b, a

    for i in range(n):
        item = a*i + b*(n-1-i)

        if len(result) == 0 or item != result[-1]:  # 由于item是递增的，可以用这种方法去重
            result.append(item)

    return result
        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    T = int(input())

    for T_itr in range(T):
        n = int(input())

        a = int(input())

        b = int(input())

        result = stones(n, a, b)

        fptr.write(' '.join(map(str, result)))
        fptr.write('\n')

    fptr.close()


```