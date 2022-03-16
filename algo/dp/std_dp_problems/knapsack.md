**KNAPSACK:**
--
Given N items and a knapsack of size W. Every item has a weight wi and profit pi associated with it (1<=i<=N).\
We can select some items from the list such that total weight does not exceed knapsack capacity and profit is max

**FRACTIONAL KNAPSACK:**
-- 
Here we can take each item in any proportion. Therefore for this problem now we can apply simple greedy strategy,\
-> sort element in decreasing order by profit/weight \
-> then take max elements u can take (we can reach total weight eq to W since we can pick any item in fraction as well)

**0/1 KNAPSACK:**
--
Here we cannot take item in proportion, we have to either take it or leave it. \
Greedy won't work here since we have to maximize profit and minimize weight so we can't define a specific criterion to pick elements so we have to dp.

dp[i][j]= out of first i items we pick some items such that total weight is j and max profit that can be obtained for this is dp[i][j]

```
BASE CASE:
   for all x>=0, f[0][x]=0 - using no items,profit is zero
   for all x>=0, f[x][0]=0 - using no weight that is none item picked till now, profit is zero
   for all x>0, y>0, f[x][y]= minus infinity
   
TRANSITION:
   We have 2 choices, pick that element or don't pick that element
   for every item, we traverse on every weight upperbound and check if adding to that bound increases profit
   Using current item i:
   A = f[i-1][t]+p[i]  where 0<=t+c[i]<=W
   A = f[i-1][t]+p[i]  where 0<=t<=W-c[i]
   Not using current item i:
   B = f[i-1][t]+0     where 0<=t+0<=W
   B = f[i-1][t]       where 0<=t<=W
   We want max so:
   f[i][w]=max(A,B) = max(f[i-1][w],f[i-1][w-c[i]]+p[i])
   
 FINAL RESULT:
   Result = max(f[n][w]) where 0<=w<=W
 ```
```cpp
#include <iostream>
#include <cstring>
#include <cmath>
using namespace std;
int main()
{
    int n, w;
    cin >> n >> w;
    int c[n + 1], v[n + 1];
    for (int i = 1; i <= n; ++i)
        cin >> c[i] >> v[i];
    ll f[n + 1][w + 1];
    memset(f, 0, sizeof(f));
    for (int i = 1; i <= n; ++i)
    {
        for (int s = 1; s <= w; ++s)
        {
            f[i][s] = f[i - 1][s];
            if (s >= c[i])
            {
                maximize(f[i][s], f[i - 1][s - c[i]] + v[i]);
            }
        }
    }
    ll res = 0;
    for (int s = 0; s <= w; ++s)
        maximize(res, f[n][s]);
    cout << res;
    return 0;
}
```

```cpp
#include <iostream>
#include <cstring>
#include <cmath>
using namespace std;
int main()
{
    int n, w;
    cin >> n >> w;
    int c[n + 1], v[n + 1];
    for (int i = 1; i <= n; ++i)
        cin >> c[i] >> v[i];
    ll f[n + 1][w + 1];
    memset(f, 0, sizeof(f));
    for (int i = 1; i <= n; ++i)
    {
        for (int s = 1; s <= w; ++s)
        {
            f[i][s] = max(f[i][s - 1], f[i - 1][s]);
            if (s >= c[i])
            {
                maximize(f[i][s], f[i - 1][s - c[i]] + v[i]);
            }
        }
    }

    cout << f[n][w];
    return 0;
}
```

**OPTIMIZING SPACE:**
--
-> Notice that we are only using i-1 th row for updating values of ith row
-> So either we can maintain 2 row dp's : dp and newdp and update newdp for ith row using dp table values which belong to i-1 th row and then assign newdp to dp
-> Or we can optimize further by just taking 1 dp row table but iterating from w to 0 (instead of 0 to w) 


**GOOD CF BLOG:**
---
[KNAPSACK CF BLOG](https://codeforces.com/blog/entry/88660)

**PROBLEM LINKS:**
--

[CF 776 DIV 3](https://codeforces.com/contest/1650/problem/F) 


   
