**FIND SHORTEST PATH FROM SOURCE TO DESTINATION SUCH THAT YOU CAN TAKE HALF THE LENGHT OF ANY 1 EDGE IN THE PATH:**
--

Idea:
--
  Since any one edge. We can consider all edges.\
  For that edge a-b\
  min(wt[a-b]+dist[1-a]+dist[b-n])
  
Complexity:
--
 -> Calculate shortest path from 2 directions using dijkstra 2 times\
 -> Then iterate over all edges 
 O(vlogv+elogv)+O(e)
  
Implementation:
--
  ```cpp
#include <iostream>
#include <algorithm>
#include <vector>
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
 
int main(){
    fast_io;
    //use normal dijsktra first 
    //use modified dijkstra then
    int n,m;
    cin>>n>>m;
    vector<vector<pair<ll,ll>>> g(n+1);
    vector<vector<pair<ll,ll>>> gr(n+1);
    for(int i=0;i<m;i++){
        ll x,y,c;
        cin>>x>>y>>c;
        g[x].push_back(mp(y,c));
        gr[y].push_back(mp(x,c));
    }
    vector<vector<ll>> d(n+1,vector<ll> (2,llmx));
    auto dijk1=[&](int s,int w){
        d[s][w]=0;
        priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> q; //we need node and distance
        q.push(mp(0,s));
        while(!q.empty()){
            ll dis=q.top().first;
            ll p=q.top().second;
            q.pop();
            if(d[p][w]!=dis){
                continue;
                //since this is outdated info
            }
            for(auto x:(w==0?g[p]:gr[p])){
                int node=x.first;
                ll wt=x.second;
                if(d[node][w]>d[p][w]+wt){
                    d[node][w]=d[p][w]+wt;
                    q.push(mp(d[node][w],node));
                }
            }
        }
    };
    dijk1(1,0);
    dijk1(n,1);
    //use meet in the middle trick
    //since every edge has the possibility to be compromised we can do in m ways
    ll ans=llmx;
    for(int i=1;i<=n;i++){
        for(auto x:g[i]){
            int a=i;
            int b=x.first;
            ll wt=x.second;
            ans=min(ans,d[a][0]+d[b][1]+wt/2);
        }
    }
    cout<<ans<<"\n";
    return 0;
}
```
