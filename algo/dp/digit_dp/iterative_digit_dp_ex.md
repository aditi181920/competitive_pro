**SOLVING A DIGIT DP PROBLEM USING ITS ITERATIVE VERSION:**
---

**1. PROBLEM:**
--
-> Find cnt of numbers in range [l,r] such that sum of its digits is a prime number. (l>=1, r<=10^18)

**2. IDENTIFYING PROBLEM AND DP STATES:**
--
-> Obviously we can't iterate through every number from l to r \
-> So which property can we count such that we don't consume too much time/memory?\
-> Sum of digits of a number cannot exceed 180 for 18 digits, so we will have to track only 180 states which will save time and memory\
-> This is the key idea behind most DP problems: identify and track a property which is finite and will help us reach the answer

-> dp[x][y][z]:\
---> x : max number of digits that our dp will support \
---> y : tight condition\
---> z : max possible sum of digits of a number

-> dp[i][0][sum] : count of suffixes that can be formed starting from index i, whose digits add up to the sum\
-> dp[i][1][sum] : count of suffixes that can be formed starting from index i, whose digits add up to the sum such that the formed suffix is not greater than corresponding suffix in i/p string 

-> **BASE CASES:** dp[n][0][0] = dp[n][1][0] = 1 [there exists 1 empty suffix with sum of its digits = 0]

-> We will move from right to left while prepending digits at every index till we finally calculate dp[0][..][..] which denotes the entire input string \
-> tight : tells if the current suffix formed includes all unbounded numbers or only the numbers less than or equal to suffix<sub>input</sub>.\
-> tight is req. here because we are prepending digits so if lets say we prepended some x (x < suff<sub>inp</sub>[i]) then the no. is already small so we can take sum of unbounded numbers from suff i+1 but if eq then we have to take bounded so it doea not exceed the current number

**3. TRANSITIONS:**
--
```sh
   
   dp[i][0][sum] = summation(d=0 to 9) dp[i+1][0][sum-d]
   dp[i][1][sum] = dp[i+1][1][sum-ss[i]]+ summation(d=0 to ss[i]-1) dp[i+1][0][sum-d]
```

**4. IMPLEMENTATION:**
```cpp
int digit_dp(string ss) {
    int n = ss.size();
 
    //empty suffixes having sum=0
    dp[n][0][0] = 1;
    dp[n][1][0] = 1;
 
    for(int i = n-1; i >=0 ; i--) {
        for(int tight = 0; tight < 2 ; tight++) {
            for(int sum = 0; sum < 200 ; sum++) {
                if(tight) {
                    for(int d = 0; d <= ss[i] - '0' ; d++) {
                        dp[i][1][sum] += (d == ss[i]-'0') ? dp[i+1][1][sum-d] : dp[i+1][0][sum-d];
                    }
                }
                else {
                    for(int d = 0; d < 10 ; d++) {
                        dp[i][0][sum] += dp[i+1][0][sum-d];
                    }
                }
            }
        }
    }
    int ans = 0;
    for(int i = 0; i < 200; i++) {
        if(isPrime(i))
        ans += dp[0][1][i];
    }
    return ans;
}

COMPLEXITY: O(digits * 2 * sum * 10)
```
