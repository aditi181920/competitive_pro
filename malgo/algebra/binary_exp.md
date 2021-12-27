BINARY EXPONENTIATION
---

Naive multiplication complexity: O(n)\
Binary exponentiation complexity: O(logn)

-> it has many applications, like it can be used with any operations that have the property of associativity ex modular multiplication,matrix multiplication etc.
  
**ALGORITHM DESCRIPTION:**

```sh
Some prop:
a^n = a.a.a.a.....a(n times)
a^(b+c) = a^b.a^c
```

IDEA:

We split work using binary representation of exponent\
For example:
```sh
3^(13)
  = 3^(1101)
  =3^(8+4+1)
  =3^8 . 3^4. 3^1
```
The number n (exponent) has exactly floor(log2n)+1 digits in base 2, the number of multiplications reduces to O(logn)\
we can also evaluate exponent simultaneously in O(logn) as exponent keeps getting double every iteration

OVERALL COMPLEXITY: O(logn)
  
**IMPLEMENTATION:**

1. Recursive:
```cpp
#define ll long long int
ll bexp(ll a, ll b){
   if(b==0)return 1;
   ll res=bexp(a,b/2);
   if(b%2)
      return res*res*a; //since multipliying numbers=adding powers if same base
                        //if mod gives 1 implies that its 1 greater than double so 
                        //exp will be obvio 2*(b/2)+1 is b was exp
   else 
      return res*res;
 //slower because of overheads of recursive calls
 ```
 
 2. Iterative:
 ```cpp
 #define m 1000000000
 #define ll long long int
 ll bexp(ll a,ll b){
     ll res=1;
     a%=m;
     while(b>0){
         if(b&1){
             res=res*a%m;
         }
         a=a*a%m;
         b>>=1;
     }
     return res;
 }
 ```
 
