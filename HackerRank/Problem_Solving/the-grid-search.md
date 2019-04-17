# 思路

模拟题  
再稿纸上画好图，注意坐标不要写错了

# 算法复杂度: 
O(n^4)


# python3代码

```
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the gridSearch function below.
def gridSearch(G, P):
    rg = len(G)
    cg = len(G[0])
    rp = len(P)
    cp = len(P[0])

    for i in range(rg-rp+1):
        for j in range(cg-cp+1):
            same = True
            for k in range(rp):
                if G[i+k][j:j+cp] != P[k]:
                    same = False
                    break

            if same:
                return 'YES'

    return 'NO'

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    for t_itr in range(t):
        RC = input().split()

        R = int(RC[0])

        C = int(RC[1])

        G = []

        for _ in range(R):
            G_item = input()
            G.append(G_item)

        rc = input().split()

        r = int(rc[0])

        c = int(rc[1])

        P = []

        for _ in range(r):
            P_item = input()
            P.append(P_item)

        result = gridSearch(G, P)

        fptr.write(result + '\n')

    fptr.close()

```