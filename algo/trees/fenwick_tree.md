**FENWICK TREE / BINARY INDEXED TREE (BIT)**
--

-> calculates the value of function f in the given range [l,r] (i.e. f(A(l), A(l+1),....,A(r)) in O(log n) time\
-> updates the value of an element of A in O(log n) time\
-> req O(n) memory i.e. same req for A\
-> the data structure is called tree as there is a nice representation of the data structure as tree, although we don't need to model actual tree with nodes and edges.\
-> **Fenwick tree** is just an array T[0...n-1], where each of its elements is equal to value of some function applied on range [g(i),i], i.e. Ti = f(Aj)[j = g(i) to i] 
where g is some function that satisfies 0<=g(i)<=i

->complexity of both sum and increase depend on the function g. Several ways for choosing g, as long as 0<=g(i)<=i for all i. \
-> Example:  g (i) = i , which is just T = A, and therefore summation queries are quite slow.\
             g(i) = 0, which corresponds to prefix sum arrays , which means that finding the sum of the range [0,i] will only take constt time, but updates are slow\
-> so we can use a special def of function g that can handle both operations in O(log n) time.

**DEFINITION OF g(i)[lowerbound of range i is currently present in]:**
--
1. ZERO-BASED INDEXING:\
--
-> T[i] = [g(i),i]\                                                                
-> replace all trailing 1 bits in the binary representation of i with 0 bits\
-> if LSB of i is 0, then g(i) =i else we take this 1 and all other trailing 1s and flip them\
-> for ex:
```sh
     g(11) = g(1011) = 1000 = 8
     g(12) = g(1100) = 1100 = 12
     g(13) = g(1101) = 1100 = 12
     g(14) = g(1110) = 1110 = 14
     g(15) = g(1111) = 0000 = 0
   
     IMPLEMENTATION:
     g(i) = i&(i+1)           //since i+1 will off all trailing bits to 0 and set last unset bit 
                             //anding will get rid of the unsetted bit that got set due to i+1 
   //this gives the lowerbound of current range... we need to subtract 1 to jump back to smaller range
   //by jumping down like this we can cover all possible ranges present in the segment [0,l]
   //for querying [l,r] subtract [0,l] from [0,r]                                                                
```
-> now we have to find a way to iterate over all j's, s.t. g(j)<=i<=j that is [g(j),j] is the ranges i will contribute to\
-> can do so by flipping the last unset bit . for ex:
```sh
            10 = 0001010
    h(10) = 11 = 0001011
    h(11) = 15 = 0001111
    h(15) = 31 = 0011111
    h(31) = 63 = 0111111                                                                
            
    IMPLEMENTATION:
    h(j) = j||(j+1)  //since j+1 will off all trailing bits to 0 and set last unset bit
                     //oring will maintain j as it was by just setting the last unset bit that got set in j+1
 ```
 
 
 **NAIVE IMPLEMENTATION OF ZERO-BASED FENWICK TREE:**
 ```cpp
 struct FenwickTree {
    vector<int> bit;  // binary indexed tree
    int n;

    FenwickTree(int n) {
        this->n = n;
        bit.assign(n, 0);
    }

    FenwickTree(vector<int> a) : FenwickTree(a.size()) {  //building the fenwick tree
        for (size_t i = 0; i < a.size(); i++)
            update(i, a[i]);
    }

    int query(int r) {                   //querying range [0,r]
        int ret = 0;
        for (; r >= 0; r = (r & (r + 1)) - 1)
            ret=f(ret , bit[r]);
        return ret;
    }

    int sum(int l, int r) {
        return query(r) - query(l - 1);
    }

    void update(int idx, int val) {          //updation 
        for (; idx < n; idx = idx | (idx + 1))
            bit[idx]=f(bit[idx], val);
    }
};
```         
**NAIVE 2D IMPLEMENTATION ARRAY:**
```cpp
struct FenwickTree2D {
    vector<vector<int>> bit;
    int n, m;

    // init(...) { ... }

    int sum(int x, int y) {
        int ret = 0;
        for (int i = x; i >= 0; i = (i & (i + 1)) - 1)
            for (int j = y; j >= 0; j = (j & (j + 1)) - 1)
                ret += bit[i][j];
        return ret;
    }

    void add(int x, int y, int delta) {
        for (int i = x; i < n; i = i | (i + 1))
            for (int j = y; j < m; j = j | (j + 1))
                bit[i][j] += delta;
    }
};
```        
2. ONE-BASED INDEXING:\
--
-> T[i] = [g(i)+1,i]\
-> def of g : toggling the last set 1 bit in the binary representation of i
```sh
     g(7) = g(111) = 110 = 6
     g(6) = g(110) = 100 = 4
     g(4) = g(100) = 000 = 0
   
     IMPLEMENTATION:
     -> last set bit can be extracted using i & (-i) //since -i is 2's complement of i which is flipping all bits to the
                                                                //left of first set bit fron right
     => g(i) = i-(i&(-i))
     -> we need to change values T[j] in the seq i, h(i), h(h(i)),... when u want to update A[j], where h(i) is defined as:
              h(i) = i+(i&(-1))                                                                
```
**NAIVE IMPLEMENTATION:**
```cpp
struct FenwickTreeOneBasedIndexing {
    vector<int> bit;  // binary indexed tree
    int n;

    FenwickTreeOneBasedIndexing(int n) {
        this->n = n + 1;
        bit.assign(n + 1, 0);
    }

    FenwickTreeOneBasedIndexing(vector<int> a)
        : FenwickTreeOneBasedIndexing(a.size()) {
        for (size_t i = 0; i < a.size(); i++)
            add(i, a[i]);
    }

    int sum(int idx) {
        int ret = 0;
        for (++idx; idx > 0; idx -= idx & -idx)
            ret += bit[idx];
        return ret;
    }

    int sum(int l, int r) {
        return sum(r) - sum(l - 1);
    }

    void add(int idx, int delta) {
        for (++idx; idx < n; idx += idx & -idx)
            bit[idx] += delta;
    }
};
``` 

**RANGE OPERATIONS:**
--

A Fenwick tree can support the following range operations:\
1. Point update and Range query (ordinary Fenwick tree)\
2. Range update and Point query

-> if we want to increment the interval [l,r] by x, we want to make 2 point updates:\
----> add(l,x) : now querying any point>=l will give x since sum from 0 to that point will be x\
----> add(r+1,-x) : now querying any point>=l and <=r will only give x becoz sum from 0 to that pt. will be x and sum from 0 to point after r (x+(-x)) will be 0 and before l will be 0

**IMPLEMENTATION:**

```cpp
void add(int idx, int val) {
    for (++idx; idx < n; idx += idx & -idx)
        bit[idx] += val;
}

void range_add(int l, int r, int val) {
    add(l, val);
    add(r + 1, -val);
}

int point_query(int idx) {
    int ret = 0;
    for (++idx; idx > 0; idx -= idx & -idx)
        ret += bit[idx];
    return ret;
}
```
                                                                
3. Range update and Range query

-> will use two BITs names B1[] and B2[], initialized with zeroes\
-> for making an increment of x in the interval [l,r]  we need to do:
```sh
    def range_add(l, r, x):
    add(B1, l, x)
    add(B1, r+1, -x)
    add(B2, l, x*(l-1))
    add(B2, r+1, -x*r))
```
-> after update (l,r,x) the range sum query returns:\
   **sum[0,i] = sum(B1,i).i-sum(B2,i)**\
   ----> this will return:
  ``` 
   | 0.i-0            |  i<l  |
   | x.i-x.(l-1)      |l<=i<=r|
   | 0.i-(x.(l-1)-x.r)| i>r   |
```
IMPLEMENTATION:
```cpp
def add(b, idx, x):
    while idx <= N:
        b[idx] += x
        idx += idx & -idx

def range_add(l,r,x):
    add(B1, l, x)
    add(B1, r+1, -x)
    add(B2, l, x*(l-1))
    add(B2, r+1, -x*r)

def sum(b, idx):
    total = 0
    while idx > 0:
        total += b[idx]
        idx -= idx & -idx
    return total

def prefix_sum(idx):
    return sum(B1, idx)*idx -  sum(B2, idx)

def range_sum(l, r):
    return prefix_sum(r) - prefix_sum(l-1)
```      
