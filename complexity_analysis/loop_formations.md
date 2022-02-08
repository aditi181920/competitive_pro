**There are some loop formations which look like they may take a lot of time but actually they are in bounds**\

1. **Looping over all elements on their multiples:**
```cpp
    for (int i=n;i>=1;i--){
      for(int j=i;j<=n;j+=i){
        ......
        }
    }
```
This actually forms a harmonic progression:\
the pattern of number of times inner loop runs is:\
n+n/2+n/3+n/4+n/5+n/6+.....+n/n\
n(1+1/2+1/3+1/4+1/5+....+1/n)\
slightly greater than nlogn but enough to pass for n<=1e6

**NOTE:**
--
-> These kind of loop formations can be used smartly over different problems to optimize them \
-> For example: finding prime factors can be done using this looping construct very efficiently:
```cpp
 for(int i=2;i<MAX;i++){
    if(!pf[i].empty()){continue;}
    for(int j=i;j<MAX;j+=i){
      int mj=j;
      while(mj%i==0){
        pf[j].push_back(i);
        mj/=i;
      }
    }
  }
  MAX: maximum allowable prime factor
```

**PROBLEM LINK:**
--
[Finding max GCD pair GFG](https://practice.geeksforgeeks.org/problems/maximum-gcd-pair3534/1#)\
[CF 766 DIV 2](https://codeforces.com/contest/1627/problem/D)
