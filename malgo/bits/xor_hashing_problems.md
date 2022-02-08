**XOR HASHING:**
--

1. **SAMPLE PROBLEM:**
--
[ABC 238 G](https://atcoder.jp/contests/abc238/tasks/abc238_g?lang=en)\
**PROBLEM:**\
-> Given queries [l,r] we have to tell whether multiplication A<sub>l</sub>\*A<sub>l+1</sub>\*....\*A<sub>r</sub> is a cubic number

**IDEAS:**\
-> We have to basically check whether cnt of all prime factors in a given range is multiple of 3\
-> How do we do this efficiently?

**SOLUTION:**\
-> the general gist is you pick an operation that resets to the identity after being applied 3 times\
-> or base 3 xor\
-> and then you do that on the factors\
-> and it'll cancel out iff its something cubed(in case of identity resetting)\
-> then you just do that 20 30 times for less error(in case of base 3 xor)

-> first, initialize a seq of (unsigned) integers H=(H<sub>0</sub>,H<sub>1</sub>,...,H<sub>N</sub>) of length N+1 with 0.\
-> then for each prime factor, do either of the following:\
-> **RESETTING TO IDENTITY:**\
-> Choose two (unsigned) integers X<sub>0</sub> and X<sub>1</sub> at random for each prime factor p. Then let X<sub>2</sub>=X<sub>1</sub> (xor) X<sub>0</sub>\
-> If the seq A has overall k prime factors p, for each i=1,2,.....,k, if the i-th occurrence of prime factor p is included in A<sub>j</sub>, then update H<sub>j</sub><-H<sub>j</sub>(xor)X<sub>i%3</sub>\
-> By designing the hash by the procedure above, it holds that "the number of each prime factor in the segment [l,r] is multiple of 3"=>"H<sub>l</sub>(xor)H<sub>l+1</sub>(xor).......H<sub>r</sub>=0"[as we will get same number of X<sub>0</sub>,X<sub>1</sub>,X<sub>2</sub> leading to cancellation of all these]\
(Note that converse does not always hold true)\
-> After performing the operation above for all prime factors p, let H' be the array of cumulative XOR, so that H'<sub>i</sub>=H<sub>0</sub>(xor)H<sub>1</sub>(xor).....(xor)H<sub>i</sub>\
-> Then for each query, it holds that "A<sub>L<sub>i</sub></sub>\*A<sub>L<sub>i</sub>+1</sub>\*.....A<sub>R<sub>i</sub></sub> is not a cubic number"=>"H'<sub>L<sub>i</sub>-1</sub> = H'<sub>R<sub>i</sub></sub>" (Again converse does not hold true)\
-> Note that there since converse does not hold true the misjudgement of type the product not being a cubic number but H'<sub>L<sub>i</sub></sub>-1=H'<sub>R<sub>i</sub></sub> may happen\
-> Let's calculate the probability of the judgement being accurate\
-> Since this hash uses XOR as operation, the operation of one bit does not affect to another bit\
-> So, we can define probability P for each bit that while A<sub>L<sub>i</sub></sub>\*A<sub>L<sub>i</sub>+1</sub>\*.....A<sub>R<sub>i</sub></sub> is not a cubic number, H<sub>l</sub>(xor)H<sub>l+1</sub>(xor).......H<sub>r</sub> for that bit is 0 leading to a misjudgement. If this misjudgement occurs in all the bits for any query, then the answer will be considered wrong.\
-> Then, the probability of being accepted for this problem is (1-P<sup>B</sup>)<sup>QT</sup>, where B bit is the size of hash value and T is the number of test cases\
-> Making a rough estimate on B=64, P=0.5(each bit has 2 digits 0/1),T=100(in this problem)and taking q according to given problem the probability of acceptance comes out to be 0.9999999, even if you take P=0.7 then still acceptance probability is still 0.995 which is still high enough

-> **XOR HASHING:**(Basically addition on mod 3(Note:3 is taken with respect to this problem, it may change))\
-> Choose a random value x as an integer in base 3=>{0,1,2} for each prime factor p\
-> Then, for each integer i from 1 through N, if A<sub>i</sub> has k prime factors p, then update as H<sub>i</sub><-H<sub>i</sub>+k\*x \
-> Again by this design of hash we can see that the number of each prime factor in the segment is multiple of 3=> H<sub>l</sub>+H<sub>l+1</sub>+....+H<sub>r</sub>=0 mod3 (as if we sum up all k\*x for all prime p then if all occur some 3 multiple times then definitely 0)\
-> Also same for each query, it holds that "A<sub>L<sub>i</sub></sub>\*A<sub>L<sub>i</sub>+1</sub>\*.....A<sub>R<sub>i</sub></sub> is not a cubic number"=>"H'<sub>L<sub>i</sub>-1</sub> = H'<sub>R<sub>i</sub></sub>" (Again converse does not hold true)\
-> But the converse is not true as 2\*cnt , 1\*cnt with mod 3 gives random values including 0 so again same misjudgement occurs as given above
-> probability P : the misjudging H'<sub>L<sub>i</sub>-1</sub> = H'<sub>R<sub>i</sub></sub> mod 3 while A<sub>L<sub>i</sub></sub>\*A<sub>L<sub>i</sub>+1</sub>\*...A<sub>R<sub>i</sub></sub> is not a cubic number\
-> suppose that we have the program that repeats this judgement B times. If the misjudgment happens in all trials for a single query, then the answer will be considered wrong.\
-> The probability of being accepted for this problem is (1-P<sup>B</sup>)<sup>QT</sup>, where B bit is the size of hash value where T is the number of test cases.\
-> Again making rough estimations on B=50, P=1/3 (since for each trial we can have 0,1,2), T=100 again acceptance comes out to be 0.99999, even which P=0.5 it is still 0.9999 \


-> If you are still worried in any of the above operations, then just repeat same operation some more times too make sure.

**NOTE:**\
-> Note the time difference in your submission for above 2 methods... 1st method actually takes significantly very less time than the 2nd because 2nd has high constt factor due to more loops for error reduction
