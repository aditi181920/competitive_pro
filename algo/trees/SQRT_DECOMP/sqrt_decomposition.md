SQRT DECOMPOSITION
--
reducing O(n) for trivial algos to O(sqrt(n))\
IDEA: splitting the input requests in sqrt blocks of length sqrt(rounding up may be required)\

```cpp
Example: Given a[0...n-1], find sum of elements a[l...r] for arbitrary l and r in O(sqrt(n)) operations.


// input data
int n;
vector<int> a (n);

// preprocessing
const int len = (int) sqrt (n + .0) + 1; // size of the block and the number of blocks
vector<int> b (len);
for (int i=0; i<n; ++i)
    b[i / len] += a[i];
int sum = 0;
int c_l = l / len,   c_r = r / len;
if (c_l == c_r)
    for (int i=l; i<=r; ++i)
        sum += a[i];
else {
    for (int i=l, end=(c_l+1)*len-1; i<=end; ++i)
        sum += a[i];
    for (int i=c_l+1; i<=c_r-1; ++i)
        sum += b[i];
    for (int i=c_r*len; i<=r; ++i)
        sum += a[i];
}
NOTE: This is just one way of using idea of sqrt decomposition, actually 
there are many other ways to implement this and use this
```                           
One of the ideas for updating elements of array can be:\
update blocks which lies completely inside range using a ds for that block requiring O(1) operation and for few elements lying outside 
we can just update them manually as they can be around 2.sqrt(n) in worst case which is not very big\
For example: let's say we can do 2 types of operations on a[i]: add element x to all values in range [l,r], query the value of a[i]\
-> for this we can just add x to block b[k] (initially b[k]=0) for those b[k] which lie inside interval [l,r] and add x to all a[i] that belong to the tails of the interval\
-> the answer to query will simply be a[i]+b[i/s] where s is block size\
--> complexty of updation will come out to be O(sqrt(n)) and query will come out to be O(1)\
If task required both range updates as well as range queries then both can be done in O(sqrt(n))\
-> will require 2 blocks for this b and c- b:keep track of element updates , c: keep track of answer to the query (that answer of range query for each block, we need to update this block for trailing a[i]'s while updation also we can set b[i] in this range back to zero just after finishing query uhmmmmm.....)

Operations like:\
-> kth largest number, adding /deleting elements, operation on subarray, check whether an element belongs to a set or not,
  finding no. of zero/non-zero elements, finding first non-zero element, counting element which satisfy a certain property

**PROBLEM LINKS:** \
[Codeforces Round 762 div 3](https://codeforces.com/contest/1619/problem/H)
