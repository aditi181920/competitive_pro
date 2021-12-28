MODULAR MULTIPLICATIVE INVERSE
--

```sh
A modular multiplicative inverse of an integer a is an integer x such that    
                     a.x ≡ 1   mod m
x is a^(-1)
also modular multiplicative inverse exists iff a and m are relatively prime (i.e. gcd(a,m) = 1).
```

FINDING MODULAR MULTIPLICATIVE INVERSE:
---

1. EXTENDED EUCLIDEAN ALGORITHM:
---

	consider an equation:         a.x + m.y = 1
	this is a linear diophantine eq in 2 variables
	when gcd(a,m)= 1 the eq has a solution which can be found using extended euclidean algo. 
	gcd(a,m) = 1 is also the condition for the modular inverse to exist
	
	if we take mod m both sides in the above eq , we get
	  a.x ≡   1 mod m 
	thus the modular inverse of a is x
	 
	int x, y;
	int g = extended_euclidean(a, m, x, y);
	if (g != 1) {
	    cout << "No solution!";
	}
	else {
	    x = (x % m + m) % m;
	    cout << x << endl;
	}
x obtained from extended euclidean may be negative that is why we add m 

2. BINARY EXPONENTIATION:
---

	Euler's theorem states that   a^(Φ(m)) ≡ 1   mod m
	where     is euler's totient function
	a and m must be relative prime
	if m is a prime number, this simplifies to Fermat's little theorem:  a^(m-1) ≡ 1   mod m
	multiplying both sides of the above eq by a^(-1) , we get:
	a^(m-2) ≡ a^(-1)    mod m
	we can find the LHS using binary exponentiation
  
3. FINDING THE MODULAR INVERSE OF EVERY NUMBER MODULO M IN O(mlogm)

```sh
	inv[1]=1
	formula : inv[i] = - floor(m/i) . inv[m mod i] mod m
  this formula can be deduced from m mod i = m-floor(m/i).i
  HINT: taking mod m both sides and multiplying i^(-1).(m mod i)^(-1) both sides
```
