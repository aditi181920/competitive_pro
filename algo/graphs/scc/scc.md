**STRONGLY CONNECTED COMPONENTS:**
--

-> These don't intersect=> they are a partition of provided vertices\
-> Condensation graph: contains all SCC as one vertex . There is an edge b/w Ci and Cj of condensation graph if and only if there exists some edge (u,v) such that u belongs to Ci and v belongs to Cj\
-> Condensation graoh is always acyclic. 
  
**Theorem:**
--

-> Let C and C' are 2 different strongly connected components and there is an edge (c,c') in the condensation graph between these two components. Then tout [c]>tout[c']

**Kosaraju's algo for finding SCC:**
--

-> Do a dfs, keep track of exit times\
-> Sort vertices in decreasing order of exit times\
-> reverse the edges and construct a reverse graph\
-> Now dfs on this reverse graph in the order of obtained exit array\
-> The components we recieve here are strongly connected \

**Proof:**
--
 One proof for this algo can be\
 -> Since we topsorted the vertices, the vertex from which we start the second dfs is always visited first and all other vertices are always reachable from this\
 -> Now we need to check reverse reachability, so we use reverse graph, whosoever vertices now are reachable (they were also reachable in normal graph). So these form SCC
 
 
 **Constructing condensation graph:**
 --
 
 -> After creating connected component, find some vertex in each component, to represent that component.\
 -> Then we connect SCC nodes if there exists some edge between any nodes of these SCC.
```cpp

struct scc{
  vector<vector<int>> g,comp,r;
  vector<int> order,who,vis;
  int cnt=0;
  int n;
  void init(int n){
    this->n=n;
    g.resize(n+1);
    comp.resize(n+1);
    who.resize(n+1,0);
    vis.resize(n+1,0);
    r.resize(n+1);
  }
  void add(int x,int y){
    g[x].push_back(y);
    r[y].push_back(x);
  }
  void topsort(int node){
    vis[node]=true;
    for(auto x:g[node]){
      if(vis[x])continue;
      topsort(x);
    }
    order.push_back(node);
  }
  void dfs_scc(int node){
    vis[node]=true;
    comp[cnt].push_back(node);
    who[node]=cnt;
    for(auto x:r[node]){
      if(vis[x])continue;
      dfs_scc(x);
    }
  }
  void build(){
    for(int i=1;i<=n;i++){
      if(!vis[i]){
        topsort(i);
      }
    }
    vis.assign(n+1,false);
    for(int i=order.size()-1;i>=0;i--){
      int x=order[i];
      if(!vis[x]){
        dfs_scc(x);
        cnt+=1;
      }
    }
  }

};
```

**TARJAN'S ALGORITHM FOR FINDING SCC:**
--

-> Just like in bridge finding, we maintain entry time (tin) and low link (low) for every vertices\
-> Now note that SCC all form cycles, and all the nodes of a SCC will have same low link values.. so we can use this fact to implement a cool algorithm.
