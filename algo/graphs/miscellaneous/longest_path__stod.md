**LONGEST PATH THAT CAN BE ACHIEVED TO REACH FROM A GIVEN SOURCE TO DESTINATION:**
--

[CSES HIGH SCORE]
You are given an directed graph with multiple edges and negative weight edges as well. You want to maximize your tour from source to destination. Once you reach destination you are not allowed to leave it though

Solution:

Doing a dfs can be very costly in a case where there are multiple paths leading to a node and every path improves then node then the dfs will visit the visited path again and again with respect to every previous unvisited node 
this will increase the complexity significantly large 

Non optimal dfs solution :

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
 
//------using pragmas------------
#pragma GCC target ("avx2")
#pragma GCC optimization ("O3")
#pragma GCC optimization ("unroll-loops")
 
 
int n,m;
vector<vector<array<ll,2>>> g;
vector<ll> val;
vector<int> visited;
vector<int> inff;
int ok=0;
void dfs(int node, ll v){
    visited[node]=2;
    val[node]=max(val[node],v);    
    for(auto x:g[node]){
        int y=x[0];
        ll curv=x[1];     
        if(visited[y]==2){   //indicates loop
            ll nxtval=v+curv;  
            if(nxtval<=val[y]){   //neg loop
                visited[y]=1;
            }else{                  //pos loop
                inff.emplace_back(y);
                visited[y]=1;
            }
        }else{ 
            if(visited[y]==1 && y!=n){
                if(val[y]<v+curv)dfs(y,v+curv);   //visit already visited path only if it improves value
            } 
            else dfs(y,v+curv);                 //visit all non visited path
        }
    }
    visited[node]=1;
}
void dfsreach(int node){                     //for checking reachability
    visited[node]=1;
    if(node==n)ok=1;
    for(auto x:g[node]){
        if(!visited[x[0]]){
            dfsreach(x[0]);
        }
    }
}
 
int main(){
    fast_io;
    cin>>n>>m;
    g.resize(n+1);
    map<pair<int,int>,ll> edg;
    map<pair<int,int>,ll> vis;
    for(int i=0;i<m;i++){
        int a,b;
        ll c;
        cin>>a>>b>>c;
        if(a==b){
            if(c<=0)continue;
            else{
                inff.push_back(a);
                continue;
            }
        }
        if(vis[mp(a,b)]==0)edg[mp(a,b)]=c;
        else
        edg[mp(a,b)]=max(c,edg[mp(a,b)]);
        vis[mp(a,b)]=1;
    }
    for(auto x:edg){
        array<ll,2> ar;
        ar[0]=x.first.second;
        ar[1]=x.second;
        g[x.first.first].emplace_back(ar);          //creating edge after removing redundancy
    }
    val.resize(n+1,llmn);
    visited.resize(n+1);
    dfs(1,0);
    visited.assign(n+1,false);
    for(auto x:inff){                     //checking reachabiltiy of all positive weight nodes
        dfsreach(x);
    }
    if(ok==1){
        cout<<"-1\n";
    }else cout<<val[n]<<"\n";
    return 0;
}
```

Optimal solution:

Note that we can change this statement a bit\
-> we want to find longest path \
-> if there is negative weight cycle we ignore it\
-> if there is a positive weight cycle then -1

Now lets change this to a shortest path problem \
-> we want to find shortest path\
-> now neg wt cycle changes to positive weight cycle and this will get ignored automatically using shortest path algo\
-> positive wt cycle changes to negative weight cycle and this can be detected easily \
-> now after we detect the neg weight edges we need to check their reachability from both source and destination 

--> we can use algorithm like bellman ford to implement this 

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
 
//------using pragmas------------
#pragma GCC target ("avx2")
#pragma GCC optimization ("O3")
#pragma GCC optimization ("unroll-loops")
 
int ok=0;
vector<bool> visited;
void dfs(int node,vector<vector<pair<ll,ll>>> &adj,int &n){
    visited[node]=true;
    if(node==n){
        ok=1;
        return;
    }
    for(auto x:adj[node]){
        if(!visited[x.first]){
            dfs(x.first,adj,n);
        }
    }
}
map<int,int> mark;
void dfsok(int node,vector<vector<pair<ll,ll>>> &adj){
    visited[node]=true;
    if(mark[node]==1){
        ok=1;
        return;
    }
    for(auto x:adj[node]){
        if(!visited[x.first]){
            dfsok(x.first,adj);
        }
    }
}
int main(){
    fast_io;
    int n,m;
    cin>>n>>m;
    map<pair<int,int>,ll> edg;
    map<pair<int,int>,ll> vis;
    vector<pair<pair<ll,ll>,ll>> g;
    vector<vector<pair<ll,ll>>> adj(n+1);
    for(int i=0;i<m;i++){
        int a,b;
        ll c;
        cin>>a>>b>>c;
        if(vis[mp(a,b)]==0)edg[mp(a,b)]=(-1)*c;
        else
        edg[mp(a,b)]=min((-1)*c,edg[mp(a,b)]);
        vis[mp(a,b)]=1;
    }
    for(auto x:edg){
        adj[x.first.first].push_back(mp(x.first.second,x.second));
        g.emplace_back(mp(mp(x.first.first,x.first.second),x.second));  //creating edges after removing redundant mutliple edges
    }
    vector<ll> dp(n+1,llmx);
    dp[1]=0;
    for(int i=0;i<m;i++){           //Bellman ford
        for(auto x:g){
            int a=x.first.first;
            if(dp[a]==llmx)continue;
            int b=x.first.second;
            ll c=x.second;
            if(dp[b]>dp[a]+c){
                dp[b]=dp[a]+c;
            }
        }
    }
    vector<ll> dp2(n+1);
    dp2=dp;
    for(auto x:g){            //relax one more time for finding negatvie weight chycle
        int a=x.first.first;
        if(dp2[a]==llmx)continue;
        int b=x.first.second;
        ll c=x.second;
        if(dp2[b]>dp2[a]+c){
            dp2[b]=dp2[a]+c;
        }
    }
    visited.resize(n+1);
    for(int i=1;i<=n;i++){        //find negative weight nodes
        if(dp[i]!=dp2[i]){
            if(!visited[i]){
                dfs(i,adj,n);       //check dest reachability
                if(ok==1)mark[i]=1;
                ok=0;
            }
        }
    }
    ok=0;
    visited.assign(n+1,false);
    dfsok(1,adj);                  //check source reachability
    if(ok==1){
        cout<<"-1\n";
    }else{
        cout<<dp[n]*(-1)<<"\n";
    }
    return 0;
}
```
