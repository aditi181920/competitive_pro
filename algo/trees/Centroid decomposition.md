**Center of a graph:**
--

**Remoteness:** Vertex remoteness is distance from its furthest node.\
**Center:** Node that minimizes remoteness. (Can be max 2 centers and min 1 center)
**Theorem:** A center always passes through the diameter
**Proof:** If c is a center having 2 subtrees with largest depth d1 and d2. So since c is a center d2 can be max d1 and min d2-1. Now if we calculate diameter including c in both cases new diameter comes out to be greater than old. So hence proved.

**Centroid of a graph:**
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

#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
#define llu long long unsigned int
#define ld long double
#define mp make_pair
mt19937 rng(chrono::steady_clock::now().time_since_epoch().count());
//-----constants---------------
const ll big=2000000000;
const ll inf=10000000;
ll llmx=1e15;
ll llmn=-1e15;
int mn=-1e8;
int mx=1e8;
const ll mod =998244353;
//const ll mod=1000000007;
ll limit=20000001;
//const ll N=200005;
const ld pi=3.1415926535;

//------using pragmas------------
#pragma GCC target ("avx2")
#pragma GCC optimization ("O3")
#pragma GCC optimization ("unroll-loops")

//-----------------using pbds--------
#include <ext/pb_ds/assoc_container.hpp> // Common file
#include <ext/pb_ds/tree_policy.hpp>
#include <functional> // for less
using namespace __gnu_pbds;
 
typedef multi_ordered_set tree<int, null_type, less_equal<int>, rb_tree_tag, tree_order_statistics_node_update> multi_set;
typedef ordered_set tree<int, null_type, less<int>, rb_tree_tag,tree_order_statistics_node_update> ordered_set;
set<int> g[100005];
int n;
vector<vector<int>> centroid;
vector<map<int,int>> calcdis;
vector<int> sz,par;
int cnt=0;
 void dfs(int node,int p){               //->calculating size of the subtrees through dfs traversal
  sz[node]=1;
  cnt+=1;
  for(auto x:tr[node]){
    if(x!=p){
      if(vis[x])continue;
      dfs(x,node);
      sz[node]+=sz[x];
    }
  }
}
int find_centroid(int  node,int p){         //-> finding centroid
  for(auto x:tr[node]){
    if(x==p)continue;
    if(vis[x])continue;
    if(sz[x]>(cnt/2)){
      return find_centroid(x,node);
    }
  }
  return node;
}
void dfsdistance(int c,int node,int p){
  for(auto x:g[node]){
    if(x==p)continue;
    if(vis[x])continue;
    calcdis[c][x]=calcdis[c][node]+1;
    dfsdistance(c,x,node);
  }
}
void create(int p,int root){                       //centroid decomposition
  cnt=0;
  dfs(root,p);                                     //->subtree sizes
  int node=find_centroid(root,p);                  //find centroid 
  if(p!=-1){
    centroid[p].push_back(node);                   //constructing centroid tree
    centroid[node].push_back(p);
  }                                                //now we need to remove every edge of type node->x and x->node removing node to x is easy for x-> node uhm
  par[node]=p;       
  vis[node]=true;
  dfsdistance(node,node,-1);                  
  vis[node]=1;
  for(auto x:tr[node]){
    if(vis[x])continue;
    create(node,x);
  }    
}

```

-> the main challenge with centroid decomposition is using this technique to solve different problems

**COMPLEXITY:**
--
O(nlogn) [logn levels+visiting n nodes in each level]


**PRACTICE PROBLEM:**
--

[CF 199 DIV2](https://codeforces.com/contest/342/problem/E)\
[IOI 2011 RACE](https://oj.uz/problem/view/IOI11_race)\
[CC PRIMEDST](https://www.codechef.com/problems/PRIMEDST?tab=statement)
