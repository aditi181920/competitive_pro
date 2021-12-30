CHINESE REMAINDER THEOREM
--

FORMULATION:
---
```sh
Let p = p1p2....pk, where pi are pairwise relatively prime (that is gcd(mi,mj)=1 whenever i not eq j). 
In addition to pi, we are given a set of congruence eq's:
     a ≡ a1 (mod p1)
     a ≡ a2 (mod p2)
     ......
     a ≡ ak (mod pk)
where ai are some given constt.
then there is a unique solution for x modulo p
```

COROLLARY:
---
```sh
A consequence of the CRT is that the eq 
    x ≡ a (mod p)
is equivalent to the system of equations
    x ≡ a1 (mod p1)
    ......
    x ≡ ak (mod pk)
(assumed that p = p1p2....pk and pi are relatively prime).
```

GARNER'S ALGORITHM:
---
-> Another conseq of CRT
> can represent big numbers using an array of small integers. \
> For example:\
> Let p = product of first 1000 primes. \
> So, p has around 3000 digits.\
> any number a less than p can be represented as an array a1,...,ak, where ai ≡ a (mod pi) (using CRT)

-> Now we need to know how to get back the number a from its representation.
```sh
Mixed Radix representation of a:
a = xkp1...p(k-1) + ... + x3p1p2 + x2p1 + x1
-> Garner's algorithm computes the coefficients x1,x2,...,xk.

Let rij denote inverse of pi modulo pj:
      rij = (pi)^(-1)  (mod pj)
-> can be found using methods for finding modular inverse

From 1st congruence equation:
a1 ≡ x1 (mod p1)

Similarly,
a2 ≡ x1 + x2p1 (mod p2)

Rewriting:
a2 - x1 ≡ x2p1 (mod p2)
(a2 - x1)r12 ≡ x2 (mod p2)
x2 ≡ (a2 - x1)r12 (mod p2)

Similarly,
x3 ≡ ((a3 - x1)r13 - x2)r23 (mod p3)

Following same pattern we can find all the coefficients in O(k^2)
```
IMPLEMENTING GARNER'S ALGO:
---
```cpp
for (int i = 0; i < k; ++i) {
    x[i] = a[i];
    for (int j = 0; j < i; ++j) {
        x[i] = r[j][i] * (x[i] - x[j]);

        x[i] = x[i] % p[i];
        if (x[i] < 0)
            x[i] += p[i];
    }
}
```

ANOTHER WAY FOR FINDING SOLUTION:
---
```sh
-> define bi = p/pi 
-> define bi' = bi^(-1) (mod mi)
->  x = (summation(i=1 to n)) aibibi' (mod p) is the unique solution
```

**Proof:** 
```sh
x = a1y1z1 + a2y2z2 + ... + akykzk
-> now for each i = 1,2,3, ... , k
    x ≡ (a1y1z1 + a2y2z2 + ... + akykzk) (mod pi)
      ≡ aiyizi  (mod pi)                           [since pi appears in all yj with j not eq i]
      ≡ ai  (mod pi)                               [since zi mod pi is equivalent to yi^(-1) mod pi
-> so this equation follows
-> showing no other solution exists modulo pq.
    let y and z be a solution for x
    if z ≡ ai(mod pi)                              (true since z is a solution)
    then z-y is a multiple of pi                   (this holds true for all i)
    => since pi's are coporime, z-y is a multiple of p1p2...pk
    => z ≡ y (mod p)
```
    
