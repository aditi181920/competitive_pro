**SEGMENT TREE AS INTERVAL TREE:**
--

-> Segment tree can be used as an interval tree in different ways \
-> Normal segment tree we can traverse from a node corresponding to segment [l,r] to  every individual node l,l+1,l+2,l+3,...r\
-> Similarly if we reverse the edges of a segment tree we can go from every smaller interval to a bigger inveral that contains it


**PROBLEM 1:**
--

The implementations may vary like:\
U may consider 2 different segment trees but then since both segments trees leafs denote the same thing there must be path between them accordingly \
U may consider single seg tree (actually 2 diff by combined by common leaf nodes ) 
In this problem, we have some [l,r] -> v (with cost w) , some v -> [l,r] (with cost w),  u->v(with cost w)\
We can use 2 segment trees (one normal, other reverse) 
1. type 3 edge: just join corresponding leaf nodes accordingly
2. type 2 edge: join from vertex v to corresponding seg node of segtree 1 (this way we can come down to any valid interval )
3. type 1 edge: join from corresponding seg node of segtree 2 to vertex v (this way we can go up to any interval and if that interval has some path to other vertex x then => v can go to x )\
-> why constructing our graph this way is useful?\
-> since now we don't need to maintain information for everything separately, we can do this smartly using intervals\

**IMPLEMENTATION:**
--
```cpp
int cur;
vector < pair < ll , ll > > v[N];
int in[SN];
int ou[SN];
void build(int l , int r , int node){
  if(l>r)return ;
    if(l == r){ //initializing leaf
        in[node] = l;
        ou[node] = r;
        return ;
    }
    in[node] = ++cur;   //indentity to segment nodes
    ou[node] = ++cur;
    int mid = (l + r) >> 1;
    build(l , mid , node + node);
    build(mid + 1 , r , node + node + 1);
    v[ou[node]].emplace_back(make_pair(ou[node + node] , 0));     //noraml seg
    v[ou[node]].emplace_back(make_pair(ou[node + node + 1] , 0));
    v[in[node + node]].emplace_back(make_pair(in[node] , 0));     //reverse seg
    v[in[node + node + 1]].emplace_back(make_pair(in[node] , 0));
}
void query(int l , int r , int node , int ql , int qr , int vertex , int type , int cost){
    if((l>qr)||(r<ql)){
        return;
    }
    if(l >= ql && r <= qr){
      (type==2?v[vertex].emplace_back(make_pair(ou[node] , cost)):v[in[node]].emplace_back(make_pair(vertex , cost)));
      return;
    }
    int mid = (l + r) >> 1;
    query(l , mid , node + node , ql , qr , vertex , type , cost);
    query(mid + 1 , r , node + node + 1 , ql , qr , vertex , type , cost);
}
int main(){
   cur=n;
   build(1,n,1);
   //add edges according to the problem
}

```

**SAMPLE PROBLEM:**
--
[CF 406 DIV 1](https://codeforces.com/contest/786/problem/B)
