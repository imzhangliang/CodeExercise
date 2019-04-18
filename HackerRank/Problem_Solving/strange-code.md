# 思路

模拟题。  
可以发现前n轮的倒计时总数为 3*(2^n-1)，  
第n轮的倒计时总数为3*(2^n-1) - 2*(2^(n-1) - 1)  
只要知道是第几轮的倒计时就好计算了

# 算法复杂度: 
O(log(n))

# python3 代码
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the strangeCounter function below.
def strangeCounter(t):
    intervals = [0]
    for i in range(1,50):   # 3*2^50 - 1应该要超过10的12次方
        if t <= 3*(2**i-1):
            currCount = t - 3*(2**(i-1)-1)      # 本轮的倒计数
            currMaxCount = 3*(2**i-1) - 3*(2**(i-1)-1) # 本轮最大有多少倒计数

            return currMaxCount+1 - currCount

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    result = strangeCounter(t)

    fptr.write(str(result) + '\n')

    fptr.close()

```

# python3 代码2
看了dicussions，还有一个更简洁的写法是：
```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the strangeCounter function below.
def strangeCounter(t):
    remain = 3
    while t > remain:
        t -= remain
        remain *= 2

    return remain+1 -t

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    result = strangeCounter(t)

    fptr.write(str(result) + '\n')

    fptr.close()

```