**LOWEST COMMON ANCESTOR:**
---

Given a tree G.
For any two vertices v1,v2 the LCA of these is a vertex v that lies on the path from the root to v1 and the path from the root to v2, and the vertex should be the lowest.\
It is obvious that their lowest common ancestor lies on the shortest path from v1 to v2. \
Also if v1 is the ancestor of v2, v1 is their lowest common ancestor and vice-versa.

**IDEA OF ALGO:**
---

-> Euler tour of the tree: Make a DFS traversal starting at the root and build a list euler which stores the order of the vertices that we visit (a vertex is added to the list when we first visit it, and after the return of the DFS traversals to its children)\
-> first[0...n-1] = for each vertex i its first occurrence in euler tour\
-> height[0...n-1] = height of each node (distance from root to it) \
-> if we clearly look at the mechanism of vertex occuring in the given euler tour then we can easily see that LCA will be node with least height in euler tour between first(v1) and first(v2)\
-> we can find the node with min height in:\
---> O(sqrt(n)) with preprocessing in O(n) time using sqrt decomposition\
---> O(log n) with preprocessing in O(n) time using seg tree\
---> O(1) with O(nlogn) build time using sparse table\


**USING BINARY UPLIFTING:**
--

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define mp make_pair
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
//-----constants---------------
ll llmx=1e15;
ll llmn=-1e15;
const ll mod =998244353;
//const ll mod=1000000007;
const int N = 5e5 + 5;
const int SN = 1 << 20;
const long long inf = 1e16 + 16;
//-----containers--------------

vector<vector<int>> g;
vector<int> depth;
void dfs(int node){
  for(auto x:g[node]){
    depth[x]=depth[node]+1;
    dfs(x);

  }
}
int main(){
  fast_io;
  int n;
  cin>>n;
  int q;
  cin>>q;
  g.resize(n+1);
  vector<int> par(n+1);
  par[1]=-1;
  depth.resize(n+1);
  for(int i=1;i<=n-1;i++){
    int x;
    cin>>x;
    g[x].push_back(i+1);
    par[i+1]=x;
  }
  vector<vector<int>> up(n+1,vector<int> (25));
  for(int k=0;k<25;k++){
    for(int i=1;i<=n;i++){
      if(k==0)up[i][k]=par[i];
      else{
        if(up[i][k-1]==-1)up[i][k]=-1;
        else up[i][k]=up[up[i][k-1]][k-1];
      }
    }
  }
  for(int i=1;i<=n;i++){
    if(depth[i]==0)dfs(i);
  }
  auto uplift=[&](int kk,int x){
    for(ll i=24;i>=0;i--){
      if((1<<i)<=kk){
        kk-=(1<<i);
        x=up[x][i];
      }
    }
    return x;
  };
  while(q--){
    int a,b;
    cin>>a>>b;
    if(depth[a]>depth[b])swap(a,b);
    int k=depth[b]-depth[a];
    b=uplift(k,b);
    if(a==b){
      cout<<a<<"\n";
      continue;
    }
    for(int i=24;i>=0;i--){
      if(up[a][i]==-1||up[b][i]==-1)continue;
      if(up[a][i]!=up[b][i]){
        a=up[a][i];
        b=up[b][i];
      }
    }
    a=up[a][0];
    b=up[b][0];
    cout<<a<<"\n";
  }
}

```
[CSES COMPANY QUERIES](https://cses.fi/problemset/task/1688)

**BLOGS:**
--

[CF BY ALexLuchianov](https://codeforces.com/blog/entry/100826)


