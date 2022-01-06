**ALGORITHMS LIVE!!!**
--

-> each cell has a range of responsibility and it is going to store the sum for that range\
-> organized by lowest one bit (range of responsibility)(for 1 size :1, for 2 size:10, for 3 size: 100, for 4 size:1000)

```sh
10000                  |
 1111      |           |
 1110         |        |
 1101      |  |        |
 1100            |     |
 1011      |     |     |
 1010         |  |     |
 1001      |  |  |     |
 1000               |  |
 0111      |        |  |
 0110         |     |  |
 0101      |  |     |  |
 0100            |  |  |
 0011      |     |  |  |
 0010         |  |  |  |
 0001      |  |  |  |  |
```  
  
prefix sums kind of behaviour:\
-> start at current cell\
-> staircase down until no bit is left (remove set bits from right to left)[this allows us to break the range into range of responsibilities and those responsible cells only rather than whole range]\
-> loop runs in atmost that no. of bits\
example : for 14 = 1011 : sum of 1011+ 1010+1000\
-> O(log n) runtime

update: lets say we want to update 9, 1001\
then we need to update 1001, 1010, 1100, 10000\
so we are basically adding 1 to lowest set bit \
finding lowest set bit: \
and a number with its two's complement (reverse all bits to the left of the first set bit encountered excluding that bit itself):\
so finding lowest set bit of i :  i &(-i)\
-> must update all cells that own us\
-> move by adding lowest one bit to current index\
-> loop runs exactly no. of off bits\
-> O(log n) runtime

**APPLICATIONS:**
--

1. COUNTING INVERSIONS:

```sh  
	INVERSIONS: if i<j and a[i]> a[j] in a given permutation
	example: 7,6,2,3,1,4,5
```    
  ```sh
  
       7 1              7 1              7 1              7 1                7 1                  7 1                  7 1
	   6 0              6 1              6 1              6 1                6 1                  6 1                  6 1
	   5 0              5 0              5 0              5 0                5 0                  5 0                  5 1
	   4 0              4 0              4 0              4 0                4 0                  4 1                  4 1
	   3 0              3 0              3 0              3 1                3 1                  3 1                  3 1
       2 0              2 0              2 1              2 1                2 1                  2 1                  2 1
	   1 0              1 0              1 0              1 0                1 1                  1 1                  1 1
    //sum=0      //sum=0+1       //sum=0+1+2      //sum=0+1+2+2     //sum=0+1+2+2+4     //sum=0+1+2+2+4+2  //sum=0+1+2+2+4+2+2
 
   idea: for every element iterating from left to right add the no. of inversions corresponding to that element

  ```
-> u can compute the prefix sums using Fenwick tree: so the runtime will be O(nlogn)
	
2. FIND KTH TALLEST:
  
```sh	
given listing of heights [1,10^6]

	height	        |1	|2	|3	|4	|5	|6  |
	no. of people	|8	|2	|10	|100    |1	|2  |
	
	-> update h (height) # (quantity)
	-> query kth tallest person [1, 10^18]
	
	log(n).log(n) = O(log ^2 n)
	b.search  query BIT
```
	
![image](https://user-images.githubusercontent.com/94597499/148382134-75977464-c201-4b41-8bbf-f1b5e2d943ff.png)

-> suppose we need to find 121 tallest person\
-> we start with 16 = 16 10000\
-> we find that 16 has 123 which is big so we go to next bit that is 1000 = 8\
-> now 8 has 123 which is also big so we go to next bit that is 100 = 4\
-> now 4 has 120 that is less that 121 so we will retain this info and we will query the upper part that is 7 to 5 inclusive\
-> now we go to next bit 10 = 2 and combining with the retained info it is 6 = 110 now we see that our left height 121-120 =1 is less that 3 so we move to next bit\
-> now we go to bit 1 with combined with retained info is 5 which has 1 which is exactly what we req \
-> so the kth tallest person is this person which height 5\
-> time complexity for BIT  is O(logn) and time complexity for binary search is O(logn)
	
3. Range update and query point
  
-> backward BIT\
-> update range [a,b] + delta\
-> query location i\
-> instead of storing value on the location we store information based on the change in the value\
-> update a by delta and b by -delta
	







