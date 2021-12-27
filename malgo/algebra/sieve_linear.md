LINEAR SIEVE
--
COMPLEXITY: O(n)\
**Adv:** Calculates the factorizations of all numbers in the segment [2:n] as a side effect\
**Disadv:** takes more memory (array of n numbers) than sieve of eratosthenes (n bits)

ALGORITHM:
---
```sh
 lp[i] : minimum prime factor for number i
 pr[] : stores list of found primes
 initialize: lp[i] = 0 for all i
 States of lp[i]:
 --> lp[i] = 0 : i is prime since no smaller factors found. So, assign lp[i] = i and add i to the end of pr[]
 --> lp[i] = 1 : i is composite and its minimum prime factor is lp[i]
 For both states update values of lp[] for numbers that are divisible by i but u must set lp[] atmost once for every number:
 ---> Consider xj = i.pj , where pj are all prime numbers <= lp[i]
 ---> set lp[xj] = pj for all numbers of this form
```


PROOF:
---
Since all values lp[] are begin modified atmost once, the runtime is gauranteed to be linear\
Every number i has exactly one representation in form:\
i = lp[i].x\
where lp[i] is the minimal prime factor of i, and x does not have any prime factor less than lp[i]\
and for each lp[i] we are finding i by multiplying diff x which is gotta be unique ?\
Now, let's compare this with the actions of our algorithm: in fact, for every x it goes through all prime numbers it could be multiplied by,
i.e. all prime numbers up to lp[x] inclusive, in order to get the numbers in the form given above.\
Hence, the algorithm will go through every composite number exactly once, setting the correct values lp[] there. Q.E.D.


IMPLEMENTATION:
---
```cpp
const int N = 10000000;
vector<int> lp(N+1);
vector<int> pr;

for (int i=2; i <= N; ++i) {
    if (lp[i] == 0) {
        lp[i] = i;
        pr.push_back(i);
    }
    for (int j=0; j < (int)pr.size() && pr[j] <= lp[i] && i*pr[j] <= N; ++j) {
        lp[i * pr[j]] = pr[j];
    }
}
```


RUNTIME:
---
There is not much difference in runtime of linear sieve and sieve of erathosthenes\
in fact it works slower than optimized versions like segmented sieve in practice\
the main advantage is the ability to find factors in linear time which can be used in many applications.\
