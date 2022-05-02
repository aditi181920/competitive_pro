**PARTITION PROBLEM:**
--

Given a number N, find number of ways to partition this number such that some condition (or no condition) is satisfied for all the partitions.
  
**DP:**
--

**DEFINITION:** dp[k][m]= number of ways to partiton k using only first m numbers satisfying this condition\
**TRANSITION:** dp[k][m]=dp[k][m-1]+dp[k-(mth number satisfying the condition][m]\
**BASE CASES:** dp[k][1] = 1     dp[1][m] =1\
**FINAL ANSWER:** dp[N][m]                                           


**PROBLEM LINK:**
--

[CF 785 DIV 2 C](https://codeforces.com/contest/1673/problem/C)
