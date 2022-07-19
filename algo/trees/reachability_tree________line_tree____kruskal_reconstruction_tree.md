**REACHABILITY TREE/ LINE TREE/ KRUSKAL'S RECONSTRUCTION TREE:**
--

--> This is mostly used for problems that ask for max/min weight between nodes, or more importantly problems that ask for finding set of nodes reachable from first k edges or whether they are reachable?


-> What is a reachability tree?\
--> For every edge we create a new auxiliary node and make this node parent of the components to which x and y belongs to . This whole becomes single connected component.\
--> Its is a rooted tree containing N+M nodes where M is the number of edges\

```cpp

struct dsu{
    vector<int> s,p;
    void init(int n){
        s.resize(n+1);
        p.resize(n+1);
        iota(p.begin(),p.end(),0);
    }
    int par(int v){
        if(p[v]==v)return v;
        return p[v]=par(p[v]);
    }
    void union_set(int x,int y,int pp){
        x=par(x);
        y=par(y);
        p[x]=pp;
        p[y]=pp;
        s[x]+=s[y]+1;
        s[y]=s[x];
        s[pp]=s[x];
        // if(s[x]>s[y]){
        //     swap(x,y);
        //     s[y]+=x;
        //     p[x]=y;
        // }
    }
};
 
int main(){
  int n,m;
  cin>>n>>m;
  int nxt=n+1;
    dsu d;
    d.init(2*n);
    vector<vector<pair<int,int>>> g(2*n+1);
    for(int i=1;i<=m;i++){
        int x,y;
        cin>>x>>y;
        if(d.par(x)!=d.par(y)){
            x=d.p[x];
            y=d.p[y];
            g[x].push_back({nxt,i});
            g[y].push_back({nxt,i});
            g[nxt].push_back({x,i});
            g[nxt].push_back({y,i});
            d.union_set(x,y,nxt);
            nxt+=1;
        }
    }
}
```
  
