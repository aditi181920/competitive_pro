BASE CASES:
```sh
dp[i][j] = matching result of s[0...i) and p[0...j)
dp[0][0] = true
dp[i][0] = false for i>0   //since empty pattern can match empty string only
dp[0][j] = dp[0][j-1] && p[j-1]=='*'    //since only sequence of empty pattern can match empty string

```
TRANSITIONS:
```sh
if p[j-1]=='*'                       //we can match any number of end characters of s so ,
                                  //dp[i][j] = (dp[i][j-1]||dp[i-1][j-1]||dp[i-2][j-1]||dp[i-3][j-1]||....||dp[0][j-1])
                                             //dp[i-1][j] = (dp[i-1][j-1]||dp[i-2][j-1]||....||dp[0][j-1])
    dp[i][j]=(dp[i][j-1]||dp[i-1][j])
    
else:

    dp[i][j]=(dp[i-1][j-1] && (p[j-1]=='?' || (p[j-1]==s[i-1])))  
    //except *, only ? and any character can be present which leads to these two cases being formed                 
```
CODE:
```sh

    bool isMatch(string s, string p) {
        int slen=s.length(), plen=p.length();
        vector<vector<int>> dp(slen+1, vector<int> (plen+1,false));
        dp[0][0]=true;
        for(int j=1;j<=plen;j++){
            if(p[j-1]=='*'){
                dp[0][j]=true;
            }else break;
        }
        for(int i=1;i<=slen;i++){
            dp[i][0]=false;
            for(int j=1;j<=plen;j++){
                if(p[j-1]=='*'){
                    dp[i][j]=(dp[i][j-1]||dp[i-1][j]);
                }else{
                    dp[i][j]=dp[i-1][j-1] && (p[j-1]=='?' || s[i-1]==p[j-1]);
                }
            }
        }
        return dp[slen][plen];
    }
    
```
LINKS:\
[Standard problem](https://leetcode.com/problems/wildcard-matching/)\
[Variation 1](https://leetcode.com/problems/regular-expression-matching/) //*can match preceeding character any number of times
