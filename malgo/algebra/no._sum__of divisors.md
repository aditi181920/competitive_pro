NUMBER OF DIVISORS / SUM OF DIVISORS
--

1. NUMBER OF DIVISORS:
---
-> Prime factorization of a divisor d has to be a subset of the prime factorization of n, therefore we need to find number of all possible subsets of prime factorization of n
```sh
Prime factorization of n : p1^e1.p2^e2.p3^e3......pk^ek where pi are distinct prime numbers, then number of divisors is:
                            d(n) = (e1+1).(e2+1)......(ek+1)
                            
-> since every prime has its power + 1 different ways of occuring(does not occur, 1 time, 2 time, ... , power time)
-> note: usually number of subsets is 2^x where x is number of elements in the subset
-> but here because of presence of repetition the formula differs from the general formula
```

2. SUM OF DIVISORS:
---
```sh
-> for single distinct prime divisor n = p1^e1 the sum is :
       1+p1+p1^2+.....+p1^e1 = (p1^(e1+1) - 1)/(p1-1)   [G.P.]

-> for two distinct prime divisors n=p1^e1.p2^e2 then the sum is :
       (1+p1+p1^2+.....+p1^e1).(1+p2+p2^2+.....+p2^e2)
       = ((p1^(e1+1) - 1)/(p1-1)).((p2^(e2+1)-1)/(p2-1))
       
-> for n = p1^e1.p2^e2......pk^ek then the sum is:
       s(n) = ((p1^(e1+1) - 1)/(p1-1)).((p2^(e2+1)-1)/(p2-1)).......= ((pk^(ek+1) - 1)/(pk-1))
       
  ```
  
  MULTIPLICATIVE FUNCTIONS:
  ---
  f(x) is a multiplicative function if f(x) satisfies **f(a,b) = f(a).f(b)** if a and b are coprime\
  -> both d(n) and s(n) are multiplicative functions
  
