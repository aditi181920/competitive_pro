**DISJOINT SPARSE TABLE :**
--

It is kind of sparse table and segtree combined \
-> Like u make the given array power of two now at every level at each node of the segment tree u store ans for [i..mid) if i <mid and [mid,i] if i >mid \
-> Every node is of length with some power of 2 and is of type [L,R) there for L will be some power of 2 and R 2^x -1 \
-> From here it is pretty easy to derive relation for L,R and mid \
-> Rest is very well explained in the following blog 

[CC DISJOINT SPARSE TABLE BLOG ](https://discuss.codechef.com/t/tutorial-disjoint-sparse-table/17404)

**IMPLEMENTATION:**
--

```cpp
int sz=1;
int n;
cin>>n;
ll p;
cin>>p;
int ht=1;
while(sz<n){
    sz*=2;
    ht+=1;
}
vector<int> a(sz+1,1); //initializing with identity element
vector<vector<ll>> disjsp(ht+1,vector<ll> (sz+5));
int range=sz,d=0;
while(range>1){
    int half=(range>>1); 
    for(int i=half;i<sz;i+=range){
        disjsp[d][i-1]=a[i-1];
        for(int j=i-2;j>=max(0,i-half);j--){
            disjsp[d][j]=(a[j]*disjsp[d][j+1])%p;
        } 
        disjsp[d][i]=a[i];
        for(int j=i+1;j<=min(sz-1,i+half-1);j++){
            disjsp[d][j]=(a[j]*disjsp[d][j-1])%p;
        }
    }
    d+=1;
    range>>=1;
}
auto query=[&](int l,int r)->int{
    int k2=32-__builtin_clz(l^r)-1;  
    int dep=(ht-1)-k2-1;
    return dep;
};
......
if(l>r)swap(l,r);
int dd=query(l,r);
ll x;
if(l==r){
    x=a[l];
}
else{int dd=query(l,r);
    x=(disjsp[dd][l]*disjsp[dd][r])%p;
}
```

[SEGPRO](https://www.codechef.com/problems/SEGPROD)
