**MOST TRICKS IN BITWISE PROBLEMS INVOLVE**
--
1. Observe how the property/definition of bitwise operation given affects the operations
2. Observe hidden pattern
3. For Xor/AND problem 1 trick that can be used is parity check:\
---> since xor/and of an odd number with any number always changes the parity but xor/and of even with any number never changes the parity
4. Keep in mind properties of xor : even times xoring a number is 0 is the most commonly used property
5. Most of the problems require bitwise xor equations to be changed into bitwise AND and bitwise OR operations
```sh
A xor B = (A|B)-(A&B)
A + B = (A|B) + (A&B)
A + B = A xor B + 2(A&B)
```
6. 
