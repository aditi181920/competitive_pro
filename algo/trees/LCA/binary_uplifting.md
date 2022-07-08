**BINARY UPLIFTING:**
---

**ALGORITHM:**
---

-> up[i][j]= 2^j-th ancestor above the node i with i=1....N,j=0...ceil(log(N))[this info allows to jump from any node to any ancestor above it in O(logn) time]\
-> we can compute this array using a DFS traversal of the tree.\
-> keep info abt time of first visit of the node and the time when we left it, this info can be used to determine if a node is an ancestor of another node\
-> if we recieve query (u,v) we can check whether one node is the ancestor of the other, if yes then this node is already the LCA.\
-> else climb the ancestors of u until we find the highest node which is not an ancestor of v\

-> let l=ceil(log(n))\
-> suppose first that i=l, if up[u][i] is not an ancestor of v, then we can assign u=up[u][i] and decrement i\
-> if up[u][i] is an ancestor then just decrement i\
-> clearly doing this for all non-negative i the node u will be desired node- i.e. u is still not an ancestor of v, but up[u][0] is\
-> answer to LCA will be up[u][0]-i.e. the smallest node among the ancestors of the node u, which is also an ancestor of v\
-> So answering LCA query will iterate i from ceil(log(n)) to 0 and checks in each iteration if one node is the ancestor of the other\
-> each query can be answered in O(logn)

**IMPLEMENTATION:**
```cpp
int n, l;
vector<vector<int>> adj;

int timer;
vector<int> tin, tout;
vector<vector<int>> up;

void dfs(int v, int p)
{
    tin[v] = ++timer;
    up[v][0] = p;
    for (int i = 1; i <= l; ++i)
        up[v][i] = up[up[v][i-1]][i-1];

    for (int u : adj[v]) {
        if (u != p)
            dfs(u, v);
    }

    tout[v] = ++timer;
}

bool is_ancestor(int u, int v)
{
    return tin[u] <= tin[v] && tout[u] >= tout[v];
}

int lca(int u, int v)
{
    if (is_ancestor(u, v))
        return u;
    if (is_ancestor(v, u))
        return v;
    for (int i = l; i >= 0; --i) {
        if (!is_ancestor(up[u][i], v))
            u = up[u][i];
    }
    return up[u][0];
}

void preprocess(int root) {
    tin.resize(n);
    tout.resize(n);
    timer = 0;
    l = ceil(log2(n));
    up.assign(n, vector<int>(l + 1));
    dfs(root, root);
}
```
**COMPLEXITY:**
---
-> Preprocessing: O(nlogn)\
-> LCA query: O(logn)

**MY IMPLEMENTATION+FINDING DIS USING LCA:**
--

```cpp
vector<vector<int>> lca,tr;
vector<int> dis,tin,tout;
void dfs_dis(int node, int p){                     //dfs to calculate distance of each node from a root(of centroid tree) in original tree
  if(p!=-1)dis[node]=dis[p]+1;
  for(auto x:tr[node]){
    if(x==p)continue;
    dfs_dis(x,node);
  }
}
int timer=0;
void calctime(int node,int p){   //cout<<"node:"<<node<<"\n";                    //calculate intime and outtimes
  tin[node]=++timer;
  lca[node][0]=p;
  for(int i=1;i<=lim;i++){ //cout<<"i:"<<i<<" "<<lca[node][i-1]<<"\n";
    lca[node][i]=lca[lca[node][i-1]][i-1];
  }
  for(auto x:tr[node]){
    if(x==p)continue;
    calctime(x,node);
  }
  tout[node]=++timer;
}
int isancestor(int x,int y){                          //ancestor function
  if(tin[x]<=tin[y] && tout[x]>=tout[y])return true;
  else return false;
}
int find_lca(int x,int y){                            //lca function
  if(isancestor(y,x))return y;
  if(isancestor(x,y))return x;
  for(int i=lim;i>=0;i--){
    if(!isancestor(lca[x][i],y)){
      x=lca[x][i];
    }
  }
  return lca[x][0];
}
int dista(int x,int y){                  //finding this is dis[x]+dis[y]-dis[lca[x,y]]-dis[lca[x,y]]
  int calc=dis[x]+dis[y];
  int lcca=find_lca(x,y); 
  calc-=2*dis[lcca];
  return calc;
}
int main(){
  dis.resize(n+1);
  dfs_dis(root,-1);    
  for(int i=0;i<=n;i++)lca[i].resize(lim+1,0);          //calculation for binary uplifting to calculate lca
  calctime(root,root);                                //-> parent must be same initially otherwise lca will be wrong why -1 does not work though?well it will work but we have to put extra conditions to handle negatives
}
```

**PROBLEM LINKS:**
---

[XENIA AND TREES](https://codeforces.com/contest/342/problem/E)

