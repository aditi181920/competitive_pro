**  Center of a graph:**
--

**Remoteness:** Vertex remoteness is distance from its furthest node.\
**Center:** Node that minimizes remoteness. (Can be max 2 centers and min 1 center)
**Theorem:** A center always passes through the diameter
**Proof:** If c is a center having 2 subtrees with largest depth d1 and d2. So since c is a center d2 can be max d1 and min d2-1. Now if we calculate diameter including c in both cases new diameter comes out to be greater than old. So hence proved.

** Centroid of a graph:**
--

**Centroid:** Node when removed minimizes largest remaining component. Centroid may or may not be same as center.
**Properties:**
1. Atmost 2 centroids
2. Remaining component <= floor(n/2) in size


**Naive algo:**
--
1. Start at the algo
2. If any of the child has subtree greater than n/2 .. implies centroid lies there we need to go to that child 
3. Reapeat until all child subtree<=n/2

*dfs complexity*

**IMPLEMENTATION:**
--

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define mp make_pair
#define ld long double
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
//-----constants---------------
ll llmx=1e15;
ll llmn=-1e15;
const ll mod =998244353;
//const ll mod=1000000007
vector<int> sz;
vector<vector<int>> g;
int n;
int dfscnt(int node,int p){
  sz[node]=1;
  for(auto x:g[node]){
    if(x==p)continue;
    sz[node]+=(dfscnt(x,node));
  }
  return sz[node];
}
int fndc(int node,int p=-1){
  for(auto x:g[node]){
    if(x==p)continue;
    if((sz[x])>(n/2)){
      return fndc(x,node);
    }
  }
  return node;
}
int main(){
  fast_io;
  cin>>n;
  sz.resize(n+1);
  g.resize(n+1);
  for(int i=0;i<n-1;i++){
    int x,y;
    cin>>x>>y;
    g[x].push_back(y);
    g[y].push_back(x);
  }
  dfscnt(1,-1);
  // for(int i=1;i<=n;i++){
  //   cout<<sz[i]<<" ";
  // }
  cout<<fndc(1,-1);
  return 0;
}
```

**Centroid decomposition:**
--

-> divide and conqueor technique\
-> this is basically decomposing our original tree into centroids\
-> given a tree we find its centroid and then remove this centroid from the tree and find centroids in newly created subtrees\
-> a centroid tree is formed 

![image](https://user-images.githubusercontent.com/94597499/174425391-df74bde3-26c7-4182-b7de-717b687a3b86.png)


**IMPLEMENTATION:**
--
```cpp
struct centroid {
  vector<vector<int> > edges;
  vector<bool> vis;
  vector<int> par;
  vector<int> sz;
  int n;

  void init(int s) {
    n = s;
    edges = vector<vector<int> >(n, vector<int>());
    vis = vector<bool>(n, 0);
    par = vector<int>(n);
    sz = vector<int>(n);
  }

  void edge(int a, int b) {
    edges[a].pb(b);
    edges[b].pb(a);
  }

  int find_size(int v, int p = -1) {
    if (vis[v]) return 0;
    sz[v] = 1;

    for (int x: edges[v]) {
      if (x != p) {
        sz[v] += find_size(x, v);
      }
    }

    return sz[v];
  }

  int find_centroid(int v, int p, int n) {
    for (int x: edges[v]) {
      if (x != p) {
        if (!vis[x] && sz[x] > n / 2) {
          return find_centroid(x, v, n);
        }
      }
    }

    return v;
  }

  void init_centroid(int v = 0, int p = -1) {
    find_size(v);

    int c = find_centroid(v, -1, sz[v]);
    vis[c] = true;
    par[c] = p;

    for (int x: edges[c]) {
      if (!vis[x]) {
        init_centroid(x, c);
      }
    }
  }
};
}
```

-> the main challenge with centroid decomposition is using this technique to solve different problems

**PRACTICE PROBLEM:**
--

[CF 199 DIV2](https://codeforces.com/contest/342/problem/E)
