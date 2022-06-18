**BOTTOM-UP SEGMENT TREE:**
--

The recursive segment tree has a very big overhead due to recursion. This can be improved by using a bottom-up segment tree.\
But note that there are some limitations on bottom up segment tree 

**IMPLEMENTATION:**
--

```cpp
#include <iostream>
#include <bits/stdc++.h>
#define mp make_pair
#define pb push_back
using namespace std;
using ll = long long int;
struct segment_tree{
    vector<int> segtree;
    int n;
    int join(int x, int y){
        return x+y;
    }
    segment_tree(int n) : n(n){   //we only need 2*n nodes since we store from n to 2*n the  original array and rest contains segment
        segtree.resize(n<<1);
    }
    void build(){                 //building seg tree bottom up
        for(int i=n-1;i>0;--i){
            segtree[i] = join(segtree[i<<1], segtree[(i<<1)|1]);
        }
    }
    void update(int pos, int val){   //now updating is simple bottom up
        pos+=n;
        segtree[pos]+=val;
        pos>>=1;
        while(pos){
            segtree[pos]=join(segtree[pos<<1],segtree[(pos<<1)|1]);
            pos>>=1;
        }
    }
    int query(int l, int r){  //now for querying note that if l is odd we know it is right child so take it and move up else just move up .. similarly for r..
        l+=n;
        r+=n;
        int ans=identity element;  //0 for sum, min for max , max for min
        while(l<=r){
        if(l&1){
          ans=join(ans,segtree[l]);
          l++;
        }
        if(!(r&1)){
          ans=join(ans,segtree[r]);
          r--;
        }
        l>>=1;
        r>>=1;
        }
        return ans;
    }
    void modifyrang(int l, int r,int v){  //kind of same like querying .. this function needs testing not tested yet also push and query pt too
        l+=n;
        r+=n;
        while(l<=r){
        if(l&1){
          aux[l]=join(segtree[l],v);
          l++;
        }
        if(!(r&1)){
          aux[r]=join(segtree[r],v);
          r--;
        }
        l>>=1;
        r>>=1;
    }
    int querypt(int p) {
        int res = t[p+n];
        for (p += n; p > 0; p >>= 1) res = join(res,aux[p]);
        return res;
      }
      void push() {
        for (int i = 1; i < n; ++i) {
          t[i<<1] += aux[i];
          t[i<<1|1] += aux[i];
          aux[i] = 0;
        }
      }
    int& operator[](int idx){     //accessing seg[i+x] using seg[i] 
        return segtree[idx + n];
    }
};
  
```
**LMITATIONS:**
--
  
1. Non-commutative combiner function:\
Bottom up implementation does not maintain the order of the segments while querying segments. Therefore any join function which is non-commutative in nature will not work correctly.\
**Workaround:** When we are checking for l it goes left to right in order and similarly for r it goes right to left in order. So we can do these operations separately and merge in the end.
```cpp
  S query(int l, int r) {
  S resl, resr;
  for (l += n, r += n; l < r; l >>= 1, r >>= 1) {
    if (l&1) resl = combine(resl, t[l++]);
    if (r&1) resr = combine(t[--r], resr);
  }
  return combine(resl, resr);
}
```
2. Bottom up approach is inflexible compared to top down. Many tricks like persistant tree cannot be implementated here.
  
  
