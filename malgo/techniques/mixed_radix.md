MIXED RADIX NOTATION
---


CONVERTING decimal notation->other base notation.. 
1. take mod with place value
2. divide with place value



CALCULATING WEIGHTS in a numeral system:

Base 2 :\
Weights - x.....8,4,2 

Base 10:\
Weights - x....1000,100,10,1

(actually all digits have same place values in these sys that is the base value but the weights are cumulative with respective to weights occuring on the right, so they get multiplied,
i.e.  for 2 it is like x...., 2\*2\*2\*2, 2\*2\*2, 2\*2, 2 like this)


FINAL ALGO:\
-to find the number that will appear at ith place - take the mod with that place value \
-repetetive division with place values - eliminates the number we just found and we can move to next weight to find its corresponding number

for example: \
             11 in decimal can be written as 1011 in binary\
             1011 is equivalent to 2^3\*1+2^2\*0+2^1\*1+2^0\*1 \
             ->taking mod by 2 will give the last digit  \
             ->dividing by 2 will reduce it to : 2^2\*1+2^1\*0+2^0\*1  \
             ->the last digit has been eliminated without affecting other digits \
             ->again the same pattern has been obtained\
             ->so we can continue the process
             
             
We have seen how mod and divide method works\
this method not only works for numeral system(decimal, binary , hex, etc...) but also for mixed radix notation

(say) i have a number with weights x,y,z \
i have to find digits for each weight such that i can form a number with this mixed based notation equivalent to some number *a*  \
then i have to convert from base 10 to this mixed base \
using the same conventions above i can easily convert *a* to a number with the given mixed base \
->take mod with weight of the ith digit and divide that weight ... repeat this process\
->mixed base notation of a should be like d4(x)(y)(z)+d3(x)(y)+d2(x)+d1

NOTE:  operate on a-1 not a because a is some number that was counted (and counting starts from 1 not 0)\
       but numeral systems start from 0 so we have to subtract 1 to account for difference in convention
       
 
 **PROBLEM LINK** \
 [Codeforces Edu 119 div2 C](https://codeforces.com/contest/1620/problem/C)
