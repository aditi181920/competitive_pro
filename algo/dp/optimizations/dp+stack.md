**OPTIMIZING DP WHERE U HAVE TO FIND MIN OR MAX OF CONSECUTIVE RANGES DECREASING FROM LEFT IN EVERY TRANSITION:**
---

-> lets say we have dp transition in which we have to find min/max for [j,i] range  for j=[1,i] for all previous dp states\
-> for example:

```sh
   dp[i] = [dp[0]*max(1,2,..,i) + dp[1]*max(2,3,...,i) + dp[2]*max(3,4,5,..,i).... + dp[i-1]*max(i) 
   similarly 
   dp[i] = [dp[0]*min(1,2,..,i) + dp[1]*min(2,3,...,i) + dp[2]*min(3,4,5,..,i).... + dp[i-1]*min(i) 
```

**Idea:** use a stack\
-> use 2 stacks:\
---> stack 1 store the a[i] (max chosen to multiply) for each corresponding dp value \
---> stack 2 store the dp value multiplied to corresponding a[i] at that step\
-> verifying transitions:\
---> if new a[i] is less that stack1.top(): then it must be less than all previous a[i]'s (because of the order we are storing the values) so we just need to push this new a[i] and 
     corresponding dp to which it should be multiplied to the corresponding stacks\
---> now if the new a[i] is greater than stack1.top() since this a[i] will be included in candidates for finding max at all previous stack elements so we have to remove elements from both stack
    until a[i] is greater than the top() element (we also need to store the sum of all previous correponding dp values multiplied to a[i] as they will get a new a[i] to which 
    they should be multiplied) and when wew have done removing them we just need to push a[i] with cumulative sum of values it needs to be multiplied with\
-> this is the mechanism how it works for ma element . for min element it is just the same just replace max with min and stack top now should be greater than new a[i] for no change  
   and for change just remove elements till top is no longer greater and do the same process
   
**PROBLEM LINK:**
--
[ABC 234 G](https://atcoder.jp/contests/abc234/tasks/abc234_g?lang=en)
