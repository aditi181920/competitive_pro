**2D PREFIX SUMS:**
--

-> A[i][j]= prefix sum for every cell in row<=i and column<=j 
```sh
prefix[i][j]=  prefix[i−1][j]+prefix[i][j−1]−prefix[i−1][j−1]+arr[i][j]
```
-> for finding value in a rectangle 
```sh
query=prefix[A][B]−prefix[a−1][B]−prefix[A][b−1]+prefix[a−1][b−1]
```

**PROBLEM LINKS:**
--

[CF 817 DIV4](https://codeforces.com/contest/1722/problem/E)

