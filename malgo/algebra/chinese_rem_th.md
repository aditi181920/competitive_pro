CHINESE REMAINDER THEOREM
--

FORMULATION:
---
```sh
Let p = p1p2....pk, where pi are pairwise relatively prime. In addition to pi, we are given a set of congruence eq's:
     a ≡ a1 (mod p1)
     a ≡ a2 (mod p2)
     ......
     a ≡ ak (mod pk)
where ai are some given constt.
```
The original form of CRT then states that the given set of congruence equations always has one and exactly one solution modulo p.

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
   


> 
