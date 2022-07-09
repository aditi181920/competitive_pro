**APPLYING THE IDEA OF BINARY UPLIFTING AND LOWEST COMMON ANCESTOR:**
--

To find some f(x) between 2 nodes in a tree
--

-> We can compute f(x) from node 1 to node 2 \
-> But how to compute this f(x) fast?\
-> We use the idea of binary uplifting\
-> While uplifting or while finding up values we can record correspondingly the function f(x) and use that f(x) while calculating lca to calculate f(x) between the nodes in log(n)

```cpp
vector<int> par,depth;
vector<vector<pair<ll,ll>>> g;
vector<vector<ll>> up(200005,vector<ll> (25)),wt(200005,vector<ll> (25));
void dfs(int node,int p){
  for(auto x:g[node]){
    if(x.first==p)continue;
    par[x.first]=node;
    wt[x.first][0]=x.second;
    up[x.first][0]=node;
    depth[x.first]=depth[node]+1;
    dfs(x.first,node);
  }
}
int main(){
//---operations for graph g
  int root=1;
  par.resize(n+1);
  depth.resize(n+1);
  up[1][0]=-1;
  dfs(root,-1);
  //now binary uplift to find max in that range
  //also we have to binary uplift to find lca 
  for(int k=1;k<25;k++){
    for(int i=1;i<=n;i++){
      if(up[i][k-1]!=-1 && up[up[i][k-1]][k-1]!=-1){
        wt[i][k]=max(wt[i][k-1],wt[up[i][k-1]][k-1]);
        up[i][k]=up[up[i][k-1]][k-1];
      }else up[i][k]=-1;
      
    }
  }
  auto uplift=[&](int x,int kk,ll &ans){
    for(ll i=24;i>=0;i--){
      if((1<<i)<=kk){
        kk-=(1<<i);
        ans=max(ans,wt[x][i]);
        x=up[x][i];
      }
    }
    return x;
  };
  auto fnd_lca=[&](int x,int y,ll &ans){
     if(depth[x]>depth[y])swap(x,y);
      //depth[y]> so uplift it to same level
      int k=depth[y]-depth[x];
      y=uplift(y,k,ans);
      int lca=x;
      if(x!=y){
        for(int k=24;k>=0;k--){
          if(up[x][k]==0 || up[y][k]==0)continue;
          if(up[x][k]!=up[y][k]){
            ans=max(ans,wt[x][k]);
            x=up[x][k];
            ans=max(ans,wt[y][k]);
            y=up[y][k];
          }
        }
        lca=up[x][0];
        ans=max(ans,wt[x][0]);
        ans=max(ans,wt[y][0]);
      }
      return lca; 
  };
```
**PROBLEM LINK:**
--

[CF EDU ROUND 3](https://codeforces.com/contest/609/problem/E)
