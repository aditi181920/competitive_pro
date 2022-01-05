PERMUTATION GROUPS
--

-> multiplication of permutations implies composition and this is not commutative\
-> for example:
```sh
   a = 1  2  3  4  5                b = 1  2  3  4  5
       3  2  5  1  4                    5  3  2  1  4
   
   ba = 1  2  3  4  5               ab = 1  2  3  4  5
        2  3  4  5  1                    4  5  2  3  1
     //permutation applide from right to left since ba => boa => i=(b(a(i)))
```
-> Symmetric group Sn - all permutations on A = {1,2,...,n} also known as the symmetric grp of degree n\
-> function composition satisfies all group axioms\
-> it is always associative\
-> since symmetric grp mapping is bijective function, it is closed,\
-> bijection leads to presence of identity element (trivial bijection assigns each element of X to itself serves as an identity for the grp)\
-> also every bijection has an inverse function that undoes its action and thus each element of a symmetric grp has an inverse 
  
1. CYCLE NOTATION:
---
  ```sh
    a  = 1  2  3  4  5  6
         3  5  1  4  6  2      =>   a = (1 3)(2 5 6)(4) (can be written in any order)
  
  -> (a1 a2 .... an) is a cycle of length n or an n-cycle
  -> Mapping: ai -> a(i+k) (mod n)
  
    //a cycle is fixing any element not appearing in it
    
    b = (1 3) = 1  2  3  4  5  6           and      c = (2 5 6) = 1  2  3  4  5  6
                3  2  1  4  5  6                                  1  5  3  4  6  2
     
           => a = bc = cb = (1 3)(2 5 6) = (2 5 6)(1 3) //4 which is fixed no longer appears
     -> multiplication is commutative since the cycles are disjoint
     -> if cycles not disjoint then no longer commutative
  ```
  
  **THEOREMS:**\
  
  1. Every permutation of a finite set can be written as a cycle or a product of disjoint cycles [a= (a1 a2...am)(b1 b2...bk)...(c1 c2...cs)]\
  2. A cycle of length l = k.m, taken to the kth power, will decompose into k cycles of length m
  ```sh
     for ex:  k=2, m=3
       (1 2 3 4 5 6)^2 = (1 3 5)(2 4 6)
  ```
  3. If the pair of cycles a=(a1 a2 ... am) and b = (b1 b2 ... bn) have no entries in common, then ab = ba\
  4. The order of permutation of a finite set written in disjoint cycle form (have disjoint subset of elements) is the least common multiple of the lengths of the cycles (length of cycle=order of cycle)\
  5. Every permutation in Sn, n>1, is a product of 2 - cycles ( also called transpositions )
  ```sh
    if a = (a1 a2 ... ak)(b1 b2 ... bt)(c1 c2 ... cs)
       a = (a1 ak)(a1 a(k-1)) ... (a1 a2)(b1 bt)(b1 b(t-1)) ... (b1 b2) ... (c1 cs)(c1 c(s-1))...(c1 c2)
      
      for ex: (3 6 8 2 4) = (3 4)(3 2)(3 8)(3 6) [this is also generating elements for the given Sn]
              (1 3 7 2)(4 8 6) = (1 2)(1 7)(1 3)(4 6)(4 8)
  ```
  6. Representation of a permutation as a product of transpositions is not unique\
  7. But the number of transpositions needed to represent a given permutations is either always even or odd\
  8. **Even permutation:** Permutation that can be expressed as an even number (even parity of transpositions) of 2-cycles (similarly odd permutations -> odd no. of 2-cycles)\
  9. Every permutation can be written as a product of adjacent transpositions of the form (a,a+1) but this representation is also not unique\
  10. Any permutation a belonging to Sn has the same parity as its inverse a^(-1)
  ```sh
  INVERSE:
    if p1 = 1  2  3  4  5  6  7  8  9  10
            3  8  5  10 9  4  6  1  7  2
      then inverse of p1 is:  1  2  3  4  5  6  7  8  9  10
                              8  10 1  6  3  7  9  2  5  4
        or we can say that if a decomposes into transpositions t1t2...tk then we have a^(-1) = tk....t2t1
  ```
  11. Product of 2 even permutations is even, product of 2 odd permutations is even, product of an even and an odd permutation is odd.\
  12. Two elements of Sn are conjugate iff they consist of the same number of disjoint cycles of the same lengths\
  13. For any integer n>=2, half of the permutations of Sn are even and half are odd\
  14. A 2-cycle is its own inverse\
  15. If epsilon = b1b2...br where b's are 2-cycles, then r is even\
  16. If a belonging to Sn and a = b1b2...br = c1c2...cs where b's and c's are 2 cycles, then r and s are both even or both odd\
  17. The set of even permutations in Sn forms a subgrp of Sn\
  18. Alternating grp of degree n: Group of even permutations of n symbols is denoted by An

        
  
  
