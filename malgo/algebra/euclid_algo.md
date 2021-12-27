EUCLIDEAN ALGORITHM
--
-> used for computing gcd
-> COMPLEXITY: O(log min(a,b))

Some things to know:
---

Given 2 non-negative integers a and b, the gcd/hcf is the:
>**gcd(a,b) = largest number which divides both a and b** \
>**gcd(a,b) = max{k| k|a and k|b}** \
| stands for divides => k|a means k divides a\
-> one number zero, other non-zero => gcd=0\
-> both zero => gcd undefined but we assume that gcd=0\
=> Rule : if one number is zero => gcd=0\


ALGORITHM:
---
> gcd(a,b)-\
> a if b=0 \
> gcd(b,a mod b) otherwise


IMPLEMENTATION:
---
1. Recursive:
```cpp
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd (b, a % b);
}
```
2. Ternary:
```cpp
int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
}
```
3. Iterative:
```cpp
int gcd (int a, int b) {
    while (b) {
        a %= b;
        swap(a, b);
    }
    return a;
}
```

PROOF
---
->since 2nd argument strictly decreases, therefore the algo will always terminate.\
-> let d = gcd(a,b)    then  d|a    and   d|b  \
       a mod b = a-b.floor(a/b) \
       so d | (a mod b) \ 
       for any 3 numbers  p,q,r , if p|q and p|r then p|gcd(q,r) \
       so d=gcd(a,b)|gcd(b,a mod b) \
similarly we can prove other side which will give us the req algo!\

RELATION BETWEEN GCD AND LCM
---
```sh
lcm(a,b)*gcd(a,b) = a*b
```
