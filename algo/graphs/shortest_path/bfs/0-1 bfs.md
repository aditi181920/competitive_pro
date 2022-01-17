**0-1 BFS**
---

**COMPLEXITY:**
---
**O(|E|)**

**ALGO:**
---
-> 1. **How bfs works?**
--
-> in bfs we always travel by level that is we travel all nodes that have a path of atleast x that is min path is x then go to nodes that have min path x+1\
-> so since we are already travelling based on levels it gives the shortest distance\

-> 2. **0-1 bfs:**
--
-> now we know that in bfs at a time in the queue 2 types of nodes are present : 1 having level x and 2nd having level x+1\
-> we always have to exhaust all nodes at level x before moving on to level  x+1\
-> so similary when in a graph with edge weights 0 and 1 at a time in queue again 2 types of nodes are present : \
-> having level u and u+1. Also we know when we are searching at level u next nodes will be at level u or u+1 \
-> if we follow the breadth first fashion of bfs: we have to exhaust all nodes at level u before moving on to level u+1\
-> therefore 0-1 bfs says that if we encounter edges with weight 0 then we have to push it to the start of the queue and if the weight is 1 then we have to push it at the end of the queue\
-> this way the queue will maintain its sorted order and we can follow bfs strategy\
-> note: its not necessary for it to be 0-1 we can apply it for any 0-y but caution we can't apply it to some x-y

**IMPLEMENTATION:**
---
```cpp
    int n,e;
    cin>>n>>e;
    vector<vector<pair<int,int>>> adj(n+1);
    for(int i=0;i<e;i++){
        int x,y,w;
        cin>>x>>y>>w;
        adj[x].push_back({y,w});
     //   adj[y].push_back({x,w});
    } 
    int d[n+1];
    for(int i=1;i<=n;i++){
        d[i]=1e8;
    }
    int s=1;
    d[s] = 0;
    vector<int> d(n, INF);
d[s] = 0;
deque<int> q;
q.push_front(s);
while (!q.empty()) {
    int v = q.front();
    q.pop_front();
    for (auto edge : adj[v]) {
        int u = edge.first;
        int w = edge.second;
        if (d[v] + w < d[u]) {
            d[u] = d[v] + w;
            if (w == 1)
                q.push_back(u);
            else
                q.push_front(u);
        }
    }
}
```
