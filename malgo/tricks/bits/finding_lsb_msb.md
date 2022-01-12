**FINDING LSB:**
--
-> Given a number x:\
-> (-x) : complement of x => except the rightmost set bit all other bits are flipped\
=> x & (-x) : will give the lsb

**SOME COOL APPLICATIONS:**
--
-> removing lsb or adding 1 to lsb\
-> finding if x is a power of 2 or not : if yes then lsb weight = x\
-> finding no. of ones in x 

**FINDING MSB(largest power of 2 less than/eq to one):**
--
**Idea:** Set all the bits to the right of the msb i.e. set all the bits present in the number(2^(i)-1). then we can just add 1 and get 1 higher msb value(2^(i+1)\
-> copy every one forward to its adjacent place then forward two consecutive ones forward covering 2 place to adj then forward 4 consective ones forward and so goes on....
```sh
   example:
   N is {1000000000000000}
   N = N|(N>>1) = 1100000000000000
   N = N|(N>>2) = 1111000000000000
   N = N|(N>>4) = 1111111100000000
   N = N|(N>>8) = 1111111111111111
   msb = (N+1)>>1
```
