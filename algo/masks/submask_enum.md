SUBMASK ENUMERATION
--

1. ENUMERATING ALL SUBMASKS OF A GIVEN MASK:
---
  -> let s be the current bitmask\
  -> no go to next bitmask do s-1\
  -> rightmost bit set will be removed and all bits to the right of it will become one\
  -> cut this mask to the highest value it can take\
  -> this will be the next submask after s in descending order
  
  ```cpp
  for(int s=m;s;s=(s-1)&m)
    ..... use s .....
  //note: if you want to use s when s =0 then u have to break it otherwise the algorithm will enter an infinite loop
  ```
  
2. ITERATING THROUGH ALL MASKS WITH THEIR SUBMASKS
---
**COMPLEXITY : O(3^(n))**\
-> used in applications like bitmask dynamic programming
```cpp
   for (int m=0;m<(1<<n);++m){     //1<<n = 2^(n) so m will iterate over all subsets
      for(int s=m;s;s=(s-1)&m){
         ... s and m ...
      }
   }
```
**PROOF FOR COMPLEXITY:**
--

1. FIRST
---
Consider the ith bit. There are exactly there options for it:
1. it is not included in the mask m (therefore not included in submask s),
2. it is not included in m, but not included in s
3. it is included both in m and s

2. SECOND
---
-> if mask m has k enabled bits, then it will have 2^k submasks.\
-> we have a total of nCk masks with k enabled bits, then the no. of combinations for all masks is:\
  (summation(k=0 to n)) nCk.2^(k)\
    = expansion of (1+2)^n\
    = 3^n
