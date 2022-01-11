**Given some number of different strings and a query string you have to construct the query string using substrings(of size >=2) of given strings**\
**dp state:**
```sh
dp[i] = 0 if we can't construct substring 0...i-1 of query string
dp[i] = 1 if we can
```
**Base Case:**
```sh
dp[0] = 1
```
**Idea:**\
we know that if a string can be constructed then it's construction can always be broken down in substring of size 2 and 3\
-> therefore we can define our dp state based on this information\
-> since we can store every substring of size 2 and 3 along with its required info we only need dp to tell us whether it is possible to construct a string of size i \
-> if yes then we can always construct a string of size i-2 or i-3 as ( i depends on these two states to be true so there must be some previous state leading to this)

**Transition:**
```sh
if dp[i]==1
    if query_str[i..i+1] is present in some given string then dp[i+2]=1
    if query+str[i..i+2] is present in some given string then dp[i+3]=1
```

**Constructing query string from dp states:**
```sh
if dp[n]=0 can't be constructed as we can't reach there in any way
else
start from i=n;
 if dp[i]=1:
    dp[i-2] or dp[i-3] must be one (both can also be, but doesn't make any diff)
    pick that dp and go there adding the information req for query_string[x-1....i-1] 
                            (x is the dp state we transtitioned to)
```                            

**PROBLEM LINK:**
[CF 764 DIV3](https://codeforces.com/contest/1624/problem/E)
                            
                            
                            
     
