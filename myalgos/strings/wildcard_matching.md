```sh
####BASE CASES:
dp[i][j] = matching result of s[0...i) and p[0...j)
dp[0][0] = true
dp[i][0] = false for i>0   //since empty pattern can match empty string only
dp[0][j] = dp[0][j-1] && p[j-1]=='*'    //since only sequence of empty pattern can match empty string

####TRANSITIONS:
if p[j-1]=='*'                       //we can match any number of end characters of s so ,
                                  //dp[i][j] = (dp[i][j-1]||dp[i-1][j-1]||dp[i-2][j-1]||dp[i-3][j-1]||....||dp[0][j-1])
                                             //dp[i-1][j] = (dp[i-1][j-1]||dp[i-2][j-1]||....||dp[0][j-1])
    dp[i][j]=(dp[i][j-1]||dp[i-1][j])
    
else:

    dp[i][j]=(dp[i-1][j-1] && (p[j-1]=='?' || (p[j-1]==s[i-1])))  
    //except *, only ? and any character can be present which leads to these two cases being formed                 
```
