**ADDITIONAL CONSTRAINT: HALF ONE EDGE IN THE PATH**
--

Idea
--
Since d[i] in dijkstra provides us with shortest path till i\
Lets modify this definition\
d[i] - shortest path till i such that 1 edge has been halved\
we have 2 transitions to calculate this\
for every node x adj to i -> either edge[x-i] is halved (we need normal d calculation here) to d[i] already has it \
following normal dijkstra rules we can easily implement this

IMPLEMENTATION
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
    for(int i=0;i<m;i++){
        ll x,y,c;
        cin>>x>>y>>c;
        g[x].push_back(mp(y,c));
     //   g[y].push_back(mp(x,c));
    }
    vector<ll> d(n+1,llmx);
    d[1]=0;
    auto dijk1=[&](){
        priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> q; //we need node and distance
        q.push(mp(0,1));
        while(!q.empty()){
            ll dis=q.top().first;
            ll p=q.top().second;
            q.pop();
            if(d[p]!=dis){
                continue;
                //since this is outdated info
            }
            for(auto x:g[p]){
                int node=x.first;
                ll wt=x.second;
                if(d[node]>d[p]+wt){
                    d[node]=d[p]+wt;
                    q.push(mp(d[node],node));
                }
            }
        }
    };
    dijk1();
    // for(int i=1;i<=n;i++){
    //     cout<<d[i]<<" ";
    // } cout<<"\n";
    //ok till here
    //now we find smallest distance using dijkstra such that exactly one node has been compromied somewhere in the path
    vector<ll> d2(n+1,llmx);
    d2[1]=0;
    auto dijk2=[&](){
        priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> q;
        q.push(mp(0,1));
        while(!q.empty()){
            ll dis=q.top().first;
            ll p=q.top().second;
            q.pop();
            if(dis!=d2[p]){
                continue;
            }
            for(auto x:g[p]){
                //now here we have cases
                //either extend from d[p]+wt/2=d2[x]
                //or extend from d2[p]+wt=d2[x]
                ll node=x.first;
                ll wt=x.second;
                if(d2[p]+wt <d2[node]){
                    d2[node]=d2[p]+wt;
                    q.push(mp(d2[node],node));
                }
                if(d[p]+wt/2<d2[node]){
                    d2[node]=d[p]+wt/2;
                    q.push(mp(d2[node],node));
                }
            }
        }
    };
    dijk2();
    // for(int i=1;i<=n;i++){
    //     cout<<d2[i]<<" ";
    // } cout<<"\n";
    cout<<d2[n]<<"\n";
    return 0;
}
```
