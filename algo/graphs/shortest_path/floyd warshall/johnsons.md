**CONCEPT OF REWEIGHING:**
--
-> Let's assume for simplicity, there are no mulitple edges and loops between the same pair of nodes in the same direction.\
-> Dijkstra's algorithm does not work very well for negative weight edges, so typically BellMan ford is used which has a worse time complexity.\
-> One idea to deal with negative edges is to "reweigh" the graph so that all weights are non-negative, and it still encodes the information of shortest paths in the original graph.\
-> We can't replace the weights with whatever we want.\
-> One way to modify the weights is to pick a vertex v, increase the weights of the incoming edges to v by some real value x, and decrease the weights of the outgoing edges from v by the same amount x. This way path that goes through v will have the same weight as before.\
-> So only affected paths are the ones that begin or end at v. But any such path will just be offset by x, and a shortest path will remain shortest.\
-> Now we want to apply this kind of vertex offset for all vertices independently in such a way that all the new weights are non-negative.

**DEFINITION:**
--
A function p:V->R is called a potential of graph G\
if for every edge (u->v) belongs to E, it holds that w(u->v)+p(u)-p(v) >=0


**JOHNSON'S ALGORITHM:**
---
-> apsp\
-> In the beginning let's assume there are no negative cycles in the graph\
-> If the graph is sparse (|E|<<Emax)[edges actually present very less than edges than can be present at max] then this algo works more efficiently than Floyd-Warshall

**1. STEPS:**
---
-> 1. Compute a potential p for the graph G\
-> 2. Create a new weighting w of the graph where w(u->v)=w(u->v)+p(u)-p(v)\
-> 3. Compute all pairs shortest path dist with the new weighting\
-> 4. Convert the distances back to the original problem, with the eq dist(u->v) = dist(u->v) - p(u) + p(v)

**STEP 3:**
--
-> Since the weights are now are non negative so we can use Dijkstra's algorithm to get correct distances\
-> We run Dijkstra's algo for every vertex u to get distance d[u][j] j=[1..n] \
-> Single run of Dijkstra takes O(mlogn)\
**COMPLEXITY:** O(nmlogn)  [Again this can be improved if u use Fibonacci heaps]

**STEP 1:**
--
-> The shortest path values themselves satisfy the requirement of a potential!\
-> Proof:
```sh
Fix some vertex s:
  Assign p(v) = dist(s->v) for all vertices v

Assume that p is not a potential
Then by definition of potentials there is some edge u->v s.t. w(u->v)+p(u)-p(v)<0
=>   w(u-v) + dist(s->u)-dist(s->v)<0
=>   w(u-v) + dist(s->u) < dist(s-v) 
this is a contradiction 
as this implies that dist(s-v) is not the shortest path anymore since we can reach v from u in less cost
==> p is a potential

But careful this proof is only correct if chosen vertex s can reach all vertices v
Otherwise we would have infinite potentials which is not allowed by the definition.
```
-> So now if we have some unreachable vertices how to find potential!!\
-> It turns out that we can create a new vertex s' and create edge s->v with weight 0 for every vertex v [since no incoming edges added no chance of creation of negative cycle]\
-> And now we can define potential based on shortest distance from s'\
-> since we have taken weight 0 of all newly create edges it won't mess up with our original graph values\
-> the property of potential is still valid if we delete some vertices and edges, so it not a problem to remove s' after we compute the potential\
-> So we can just run Bellman-Ford once on the graph with the new vertex s to find shortest distance which will give potential\
**COMPLEXITY:** O(mn)

-> Step 3 is the bottleneck and overall complexity of Johnson's algorithm


**OVERALL COMPLEXITY:** O(nmlogn) [O(n^2 logn+nm) if using Fibonacci heap]


**JOHSONS ALGO WITH DIJKSTRA USING PRIORITY QUEUE:**
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
#define mp make_pair
ll binexp(ll a,ll b){
    ll res=1;
    while(b>0){
        if(b&1){
            res*=a;
            res%=mod;
        }
        a*=a;
        a%=mod;
        b>>=1;
    }
    return res;
}
bool cmp(int x,int y){
    if(1) return true;
    else return false;
}
multiset<int,decltype(&cmp)> ms(&cmp);
 
 
void dfs(int node,vector<vector<pair<int,int>>> &g,vector<bool> &vis){
    vis[node]=true;
    for(auto x:g[node]){
        if(!vis[x.first]){
            dfs(x.first,g,vis);
        }
    }
}
int main(){
    fast_io;
    int t;
   // cin>>t;
   t=1;
    while(t--){
        int n,m;
        cin>>n>>m;
        int q;
        cin>>q;
        vector<ll> d(n+2,llmx);
        //bellman ford
        //at each iteration produce relaxation along each edge
        //for every edge (a,b) improve d[b]=d[a]+c
        //n-1 relaxations are enough
        //since we have n nodes
        //and 1 edge value at 0th relaxation
        //then doing n-1 relaxations corrects everything 
        vector<pair<pair<int,int>,int>> edg;
        vector<vector<pair<int,int>>> g(n+2);
        for(int i=0;i<m;i++){
            ll x,y,c;
            cin>>x>>y>>c;
            if(x==y)continue;
            edg.emplace_back(mp(mp(x,y),c));
       //     edg.emplace_back(mp(mp(y,x),c));
            g[x].emplace_back(mp(y,c));
            g[y].emplace_back(mp(x,c));
        }
        m=edg.size();
        //let's use single source shortest path 
        //bellman ford for every vertex n
        //bellman ford complexity is O(mn)
        //for every node it will be n^2 m
        //n^4 => no it is bad
        //how about johsons algorithm
        //we need belman ford for computing potentials n*m=> n*n*n
        //then we need to run dijkstra at every node
        //n* nlogm ... okkk
        //how to compute potentials
        //shortest path itself satisfies the property of potentials
        //prove:
        //potential def: for edge u->v:  w(u->v)+p(u)-p(v) >=0
        //say shortest path does not satisfy
        //w(u->v)+dis(u)-dis(v)<0
        //w(u->v)+dis(u)<dis(v)
        //this is a contradiction
        //making a new temporary source is only required only when there are some unreacheable vertices 
        //then we take another auxiliary node and connect them to unreachable component representatives
        //do bellman ford from node 1
        //ok so we need dfs as well for connecting to unreachable nodes
        vector<bool> vis(n+2,false);
        int s=n+1;
        d[s]=0;
        for(int i=1;i<=n;i++){
            if(!vis[i]){
                dfs(i,g,vis);
                edg.emplace_back(mp(mp(i,s),0));
       //         edg.emplace_back(mp(mp(s,i),0));
            }
        }
        for(int k=0;k<n-1;k++){
            for(auto x:edg){ 
                if(d[x.first.first]==llmx)continue;
                if((d[x.first.first]+x.second)<d[x.first.second]){
                    d[x.first.second]=d[x.first.first]+x.second;
                }
            }
        }
        //now we have potentials 
        //reweight each edge using potention
        //increase potential at incoming and dec at outgoing
        //w(u,v) = w(u,v)+p(u)-p(v)
        for(auto &x:edg){
            x.second=x.second+d[x.first.first]-d[x.first.second];
        }
        //now we don't have any negative edge weight
        //do dijkstra on every node
        ll ans[n+1][n+1];
        for(int i=0;i<n+1;i++){
            for(int j=0;j<n+1;j++){
                ans[i][j]=0;
            }
        }
        for(int i=1;i<=n;i++){ 
            //using i as source
            ll dis[n+2];
            for(int i=0;i<n+2;i++){
                dis[i]=llmx;
            }
            dis[i]=0;
            priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> q;
            q.push(mp(0,i));
            while(!q.empty()){
                int p=q.top().second;
                ll dd=q.top().first;
                q.pop();
                if(dd!=dis[p])continue;
                for(auto x:g[p]){
                    if(dis[x.first]> dis[p]+x.second){
                        dis[x.first]=dis[p]+x.second;
                        q.push(mp(dis[x.first],x.first));
                    }
                }
            }
            //store these values
            for(int j=1;j<=n;j++){
                if(i==j){
                    ans[i][j]=0;
                }else{
                    ans[i][j]=dis[j];
                }
            }
        }
        //convert distance back acc to original problem
        for(auto &x:edg){
            x.second=x.second-d[x.first.first]+d[x.first.second];
        }
        //now answer queries however
        while(q--){
            int x,y;
            cin>>x>>y;
            if(ans[x][y]==llmx){
                cout<<"-1\n";
            }else{
                cout<<ans[x][y]<<"\n";
            }
        }
    }
    return 0;
}
```

