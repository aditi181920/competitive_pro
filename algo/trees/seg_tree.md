SEGMENT TREE
--

-> range queries on mutable arrays (array elements can be changed without precomputing whole seg tree again)\
-> COMPLEXITY: O(log n)\
-> linear memory needed (4n for std. seg tree with array size of n)
  
STRUCTURE:
---
  
-> Root: segment a[0...n-1]\
-> each vertex (except leaf) has exactly two child vertices partitioning parent segment into two equal halves.\
-> ex: a = [1,3,-2,8,-7]:
 ```sh                 
                       a[0....4]
                         sum=3
                     /            \ 
              a[0...2]           a[3...4]
               sum=2               sum=1
           /       \            /       \
        a[0...1]   a[2...2]  a[3...3]  a[4...4]
        sum=4        sum=-2   sum=8     sum=-7
    /        \
  a[0...0]  a[1...1]
  sum=1       sum=3
```
-> ht of seg tree: O(log n)\
-> 1 + 2 + 4 + ..... + 2^(ceil(log2n)) < 2^((ceil(log2n))+1)< 4n

CONSTRUCTION:
---
  
-> decide:\
---> value to be stored at each node\
---> how to merge siblings\
-> leaf vertex value eq to corresponding element a[i]\
-> operates recursively from root vertex to the leaf vertices\
-> if called on a non-leaf vertex:\
---> recursively construct the values of the two child vertices\
---> merge the computed values of these children\
**TIME COMPLEXITY: O(n)**\
-> the merge operation is constant time (it gets called n times, which is eq to the no. of internal nodes in the seg tree).
  
QUERING SEGMENTS:
---
  
-> a[l..r] in O(log n) time\
-> if we are currently at segment a[tl....tr]. There are three possible cases:\
----> a[l...r] = a[tl...tr]  we found req ans, just return the precomputed sum stored in the vertex\
----> a[l...r] falls completely into the domain of either the left or the right child. We need to move on to that child\
----> a[l...r] intersects both children. We need to make 2 recursive calls, one for each child and combine answers recieved from both of them\
**TIME COMPLEXITY: O(log n)**\
-> at each level max of 4 calls can be made
> if current level has 4 calls then 2 middle seg can't be called further because segment is a continuous subseq so they must be included
  so only end seg's can be called\
  => will never exceed 4

POINT UPDATION:
---

-> assign a[i]=x\
-> have to update nodes to which a[i] contributes in the seg tree, i.e. seg that lie in the path from a[i] to root\
-> reach a[i] from root by calling recursively then update seg encountered when calls return
  
IMPLEMENTATION:
---
  
-> 1 based indexing:
> Parent: i\
  Left child: 2i\
  Right child: 2i+1

-> 0 based indexing:
> Parent: i\
  Left child: 2i+1\
  Right child: 2i+2
    
=> we only need one array which contains result of all segments and the tree is defined implicitly\
-> there may be some elements in array which don't correspond to any vertices in the actual tree but that does not get in our way for implementation and is more convinient\
-> we will go with 1 based indexig

```cpp
int n, t[4*maxn];

void build(int a[], int v, int tl, int tr) {  //v=1, tl=0, tr=n-1
    if (tl == tr) {
        t[v] = a[tl];
    } else {
        int tm = (tl + tr) / 2;
        build(a, v*2, tl, tm);
        build(a, v*2+1, tm+1, tr);
        t[v] = f(t[v*2], t[v*2+1]);
    }
}

int fun(int v, int tl, int tr, int l, int r) {  //for query
    if (l > r) 
        return 0;
    if (l == tl && r == tr) {
        return t[v];
    }
    int tm = (tl + tr) / 2;
    return fun((v*2, tl, tm, l, min(r, tm))
           , fun(v*2+1, tm+1, tr, max(l, tm+1), r));
}

void update(int v, int tl, int tr, int pos, int new_val) {
    if (tl == tr) {
        t[v] = new_val;
    } else {
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            update(v*2, tl, tm, pos, new_val);
        else
            update(v*2+1, tm+1, tr, pos, new_val);
        t[v] = t[v*2] + t[v*2+1];
    }
}
```

MEMORY OPTIMIZATION:
---
-> To deal with redundancy in this implementation which follows level order traversal:\
-> we renumber the vertices of the tree in the order of an euler tour traversal (pre-order preorder traversal)\
-> 
                  
                     
          
