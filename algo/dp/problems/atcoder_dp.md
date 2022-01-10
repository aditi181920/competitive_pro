**COMBINATORICS:**
--
1. [ABC 234 F](https://atcoder.jp/contests/abc234/tasks/abc234_f?lang=en)\
-> find in a given string s how many diff string can be obtained as a permutation of a non-empty, not necessarily contiguous subsequence of S?\
-> Solution: dp + combinatorics\
--> Approach 1:
```sh
   dp[i][j]: number of subseq of S consisting of first i alphabets and of length j, and their permutations
   ans for i alphabets will be : dp[i][1]+..dp[i][n]
   we have to consider all 26 alphabets so answer will be: dp[26][1]+dp[26][2]+....dp[26][n]
   lets say i know answer for alphabet a now i want to take b also and find answer
   no of ways for strings of length j having  a and b as valid characters:
    (fix 0 b)*no. of ways for having a's in j length + (fix 1 b)*no. of ways for having a's in j-1 length + .... + (fix min(freq[b],j)=k b)*no. of ways for having a's in j-k length
    => our transition becomes :
    dp[i][j] = summation(k=0 to min(j,freq[i]) dp[i-1][j-k] * jCk
```







**SOME RANDOM DP PROBLEMS:**
--
2. [ABC 234 G](https://atcoder.jp/contests/abc234/tasks/abc234_g?lang=en)
