**COMMON TRICKS:**
--
-> If we have to check equality of two arrays then common trick to proceed is take difference of them and check if it is zero, this way we only have 1 array values to maintain and check now\
--> Above trick can also be extended to some range update properties like:\
---> if we are doing std range additions then change in x<sub>n</sub>-x<sub>n-1</sub> is zero pts(x<sub>n</sub> and x<sub>n-1</sub> are inside range)\
---> similarly let's say we are adding fibonnaci numbers now that is (X<sub>l</sub>=F1, X<sub>l+1</sub>=F2, X<sub>r</sub>=F<sub>r-l+1</sub>) then change in x<sub>n</sub>-x<sub>n-1</sub>-x<sub>n-2</sub> is zero , we can prove this by property of fibonnaci numbers (f<sub>i</sub>=f<sub>i-1</sub>+f<sub>i-2</sub>)\
-> 0/1 trick: where we can generalise things to 0 and 1 and then solve\
-> reduce xor,addition to bitwise operations\
-> whenever we are asked for something related to cyclic permutation, we can most of the time construct an array 2\*n from n sized array and do sliding window\
->abs(x)=max(-x,x) trick\
---> we can expand the abs in this way and this leads to creation of some limited cases in some problems which helps a lot \
---> sample problem: [798 div2](https://codeforces.com/contest/1689/submission/161362525)\
-> cancelling trick: so there are some problems where we can just manipulate the total weights in some smart way such that we can either check that their sum, parity etc. For example in this problem we can take advantage of node degrees to maintain equality of weights. [CodeTON Round 1 (Div. 1 + Div. 2, Rated, Prizes!)](https://codeforces.com/contest/1656/problem/E)



**OPTIMIZATIONS:**
--

-> unorodered_map are hackable due to the fact that they are based on hash maps which does not perform very well in worst case because of large number of collisions.\
so map which are based on red-black trees are preferred\
-> order of cost : div>mul>abs>add,sub,compare  ..... div is 10 times add, mult 4 times add and pow being the costliest is 100 times the cost\
-> if u can make some data structures global then make it so in case u need a lot of memory and there are a lot of chance of stack overflow... but global space is vulnerable so be 
cautious as well
-> pass things by reference in functions for speed uo if u can\
-> div by const is well optimized by compilers\
-> computation of pre and post operators is done after encouter of semicolon. (so, value of a variable with pre post or none will be same until it encouters semicolon)\
-> vector takes more memory and time than array ... prefer array over vectors\
-> declare variables globally if can\
-> always pass by reference.. missing this out can actually cause a TLE when it should not\

