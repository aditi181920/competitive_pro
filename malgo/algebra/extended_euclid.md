EXTENDED EUCLIDS\'S ALGORITHM
--

this finds a way to represent gcd in terms of a and b, i.e. coefficients x and y for which:
> a.x + b.y = gcd(a,b)
  
ALGORITHM
---
```sh
x = y1
y = x1 - y1.floor(a/b)
```

-> euclidean algo ends with b=0 and a=g.  then   g.1 + 0.0 =g\
-> starting from these coefficients (x,y) = (1,0) , we can go backwards up the recursive calls by figuring out how the coefficients x and y change during the transition from (a,b) to (b, a mod b). 

 PROOF
 ---
 >say (x1, y1) for (b,a mod b)   then \
     b.x1 + (a mod b).y1 = g \
and we want to find the pair (x,y) for (a,b) s.t. a.x + b.y = g \
      a mod b = a - floor(a/b).b \
  after substitution  \
     g = b.x1 + (a - floor(a/b).b).y1 \
  rearranging \
     g = a.y1 + b(x1-y1.floor(a/b)) \
so  \
    x = y1 \
    y = x1 - y1.floor(a/b) 
  
IMPLEMENTATION
---
1. Recursive:
```cpp
int gcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
\\ this implementation produces correct result for negative integers as well
```
2. Iterative:
```cpp
int gcd(int a, int b, int& x, int& y) {
    x = 1, y = 0;
    int x1 = 0, y1 = 1, a1 = a, b1 = b;
    while (b1) {
        int q = a1 / b1;
        tie(x, x1) = make_tuple(x1, x - q * x1);
        tie(y, y1) = make_tuple(y1, y - q * y1);
        tie(a1, b1) = make_tuple(b1, a1 - q * b1);
    }
    return a1;
}
```
