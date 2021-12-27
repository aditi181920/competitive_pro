SIEVE OF ERATOSTHENES
--

-> Algorithm for finding all prime numbers in a segment [1:n]\
-> COMPLEXITY: O(nlognlogn)

IDEA
---
Every time we encounter an unmarked number we mark all its multiples in the range\ 
Marked number => Composite\
Unmarked number => Prime

PROOF
---
FUNDAMENTAL THEOREM OF ARITHMETIC :\
Every number can be written in the form of one or more primes\
So if a number has no prime(except 1) less than itself then it follows the def of prime and has to be a prime

IMPLEMENTATION
---
```cpp
int n;
vector<bool> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i <= n; i++) {
    if (is_prime[i] && (long long)i * i <= n) {
        for (int j = i * i; j <= n; j += i)  //starting from i*i is an optimization
            is_prime[j] = false;
    }
}
> i*i optimization:
any multiple of i less that i*i will have another prime whose it is a
multiplication so it must have already been visited

```

OPTIMIZATIONS
---
1. Sieving till root\
since we start from square of a number if square exceeds range then we can just stop at that number
```cpp
int n;
vector<bool> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i * i <= n; i++) {
    if (is_prime[i]) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
\\complexity does not change much but number of operations reduce significantly
```
2. Sieving by odd numbers\
since all even numbers get marked by 2 no even number can ever be prime and all its multiples were also marked by 2 so it is redundant to visit again

3. Segmented sieve \
LATER
