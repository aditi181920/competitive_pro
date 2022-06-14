**HASHING:**
--

-> Comparing strings-> O(min(n1,n2))\
-> String hashing: map each string into an integer and comparae those instead of the strings. O(1) complexity.\
``` Hash function: if 2 strings s and t are equal (s==t), then also their hashes have to be equal (hash(s) == hash(t))```\
**Note:** If the hashes are equal (hash(s) = hash(t)), then the strings do not necessarily have to be equal(collision case) (this is because of huge number of strings present which can't be distinuished using 64bit integer then)\
Of course, we want hash(s) not equal to hash(t) to be very likely if s not equal to t.\
-> Hashing is not 100% deterministically correct, because 2 complete different strings might have the same hash(hashes collide).\
-> But the probability of this collision is very low so it can be safely ignored.
                                                                                                             
**1. POLYNOMIAL ROLLING HASH FUNCTION:**
--

![image](https://user-images.githubusercontent.com/94597499/173589160-006e0fc7-aca2-4bf5-8981-099797e1970f.png)


-> p a prime number roughly equal to the number of characters in the input alphabet (distinct characters not all).\
-> m should be large since probability of 2 random strings colliding is about 1/m (some large prime like 10^9+9 is recommended)
                                                                                                                             
**Calculating probability of hash collision:**

-> Out of k randomly generated values where each value is a non-negative integer less than n, what is the probability that at least 2 of them are equal?\
--> Given a space of n possible hash values, suppose you've already picked a single value.\
--> After that, there are n-1 remaining values, that are unique\
--> Probability of generating 2 integers that are unique from each other is ```(n-1)/n```\
--> Then we have n-2 remaining values , so generating three numbers uniquely is ```((n-1)/n)*((n-2)/n)```\
--> So the probability of randomly generating k integers that are all unique is: ```((n-1)/n)*((n-2)/n)...*((n-(k-1))/n)```\
--> the above expression is approximately equal to: ```e^((-k *(k-1))/(2*n))```\
--> the probability of collision occurence:
![image](https://user-images.githubusercontent.com/94597499/173592653-a0a0331a-697a-4749-9310-0f41838e8f46.png)

![image](https://user-images.githubusercontent.com/94597499/173601621-41d31605-e071-4790-8124-d524affe3656.png)

                                                                                                            
