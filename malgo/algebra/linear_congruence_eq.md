LINEAR CONGRUENCE EQUATION
--

-> this equation is of the form:
```sh 
     a.x = b (mod n)
 a,b,n are given integers
 x is an unknown integer
```
-> req.ed to find the value of x from the interval [0,n-1]\
-> on the entire number line, there can be infinitely many solutions that will differ from each other in n.k, where k is any integer\
-> if solution is not unique, then we'll consider how to get all the solutions.

FINDING SOLUTION BY:
---

1. INVERSE ELEMENT
---

-> if a and n are coprime (gcd(a,n)=1). 
```sh
Then we can find a^(-1) and multiply both sides of the eq to get:
   x = b.a^(-1)  (mod n)
```
-> if a and n are not coprime (gcd(a,n)≠1). \
---> let g = gcd(a,n)
```sh
No solution exists if:
b is not divisible by g

Proof: for any x the left side of the equation  a.x (mod n) is always divisible by g, while the right-hand side is not divisible by
it then it follows no solution.
```

```sh
if g divides b, then by dividing both sides of the eq. by g, new eq becomes:
          a'x = b'  (mod n')
where a' and n' are already relatively prime.
so we can find x from this equation now.
```

-> it can be shown that the original equation has exactly g solutions
```sh
       xi = (x' + i.n') (mod n) for i = 0.....g-1
where x' is the x obtained just above
```
-> the number of solutions of the linear congruence equation is equal to either g = gcd(a,n) or to zero.

2. EXTENDED EUCLIDEAN ALGORITHM:
---

Converting the linear congruence equation of the following diophantine equation:
```sh
        a.x + n.k = b
    where x and k are unknown integers
```
-> can solve this equation now
