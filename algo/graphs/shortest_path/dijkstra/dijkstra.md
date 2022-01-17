**SINGLE SOURCE SHORTEST PATH ON DIRECTED/UNDIRECTED GRAPH WITH NON NEGATIVE WEIGHTS**
--

**1. NOTATIONS:**
--
-> d[v] : current length of the shortest path from s to v in d[v]. \
-> Initially, d[s] =0  , d[v] = infinity for v not eq. to s\
-> u[v] : whether vertex is marked or not \
-> Initially, u[v] = false\

**2. ALGO:**
--
-> At each iteration a vertex v is chosen as unmarked vertex which has the least value d[v]\
-> The selected vertex v is marked \
-> From vertex v relaxations are performed: all edges of the form (v,t) are considered and for each vertex t the algo tries to improve the value d[t].\
-> d[t] = min(d[t],d[v]+len) //len=length of current edge(v->t)
-> after n iterations the values of d[v] are length of shortest path from s to all vertices v.
-> unreachable vertex will have infinity after algo ends and even where they are selected in some iterations no useful work will be done since there is no adjacent edge present\
-> so we can break once we have found some unreachable vertex \

**3. RESTORING THE SHORTEST PATH:**
--
-> p[]: array of predecessors in which for each vertex v not eq s , p[v] is the penultimate vertes in the shortest path from s to v.\
-> if we take the shortest path to some vertex v and remove v from this path, we'll get a path ending in at vertex p[v] and this path will be the shortest for the vertex p[v]\
-> Shortest path: (s,...,p[p[p[v]]],p[p[v]],p[v],v)\
-> building p[]: for each succesfull relaxation update p[t] = v

**4. PROFF:(my understanding)**
--
-> After any vertex v becomes marked, the current distance to it d[v] is the shortest and will no longer change\
-> **prove by induction:**\
-> true for base case that is d[s] = 0 (the only shortest path from s to s)\
-> Suppose that it is true for some already marked vertices let's prove that it is not violated after the current iteration completes\
-> let's say x shortest paths have already been marked and the next nearest node is now y \
-> since x shortest paths have been marked the nodes that are connected with any of these marked nodes would have already been updated by the shortest path which leads through any of these marked nodes to them\
-> now if y is next nearest => any other node has greater distance will definitely have gretaer dist so they can't contribute to y in any way possible and all shorter paths have already contributed so what y have is shortest
  
**5. TIME COMPLEXITY:**
--
-> depends on implementation\
-> worst case: O(v^2) on bad implemetation\
-> worst case: O((v+e)logv) on good implemetation (v+e total traversals since we are traversing in sorted order we can say this and logv for updation) [in dense graph when e>>v then this is equivalent to O(elogv)]\
-> worst case can be reduced to even smaller using fibonnaci heap though

**6. IMPLEMENTATIONS:**
--
-> SOME GOOD IMPLEMENTATION TRICKS:\

-> **set**: based on red-black trees\
-> can use set to store d[] \
-> use pair : distance, index of vertex \
-> pairs will get automatically sorted by their distances\
-> we can just remove vertices already marked from this set so we won't need u[] either\

```cpp
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

void dijkstra(int s, vector<int> & d, vector<int> & p) {
    int n = adj.size();
    d.assign(n, INF);
    p.assign(n, -1);

    d[s] = 0;
    set<pair<int, int>> q;
    q.insert({0, s});
    while (!q.empty()) {
        int v = q.begin()->second;
        q.erase(q.begin());

        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                q.erase({d[to], to});
                d[to] = d[v] + len;
                p[to] = v;
                q.insert({d[to], to});
            }
        }
    }
}
```
-> priority_queue : based on heaps\
-> we can't remove desired elements from priority_queue \
-> we don't delete old pair of queue so we have to distinguish between old and desired pairs\
-> desired pairs: first element is eq to corresponding value in d[] all other pairs are old\
-> priority_queue by default sorts elements in descending order.\
-> to make it ascending either negate distances or pass diff sorting function

```cpp
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

void dijkstra(int s, vector<int> & d, vector<int> & p) {
    int n = adj.size();
    d.assign(n, INF);
    p.assign(n, -1);

    d[s] = 0;
    using pii = pair<int, int>;
    priority_queue<pii, vector<pii>, greater<pii>> q;
    q.push({0, s});
    while (!q.empty()) {
        int v = q.top().second;
        int d_v = q.top().first;
        q.pop();
        if (d_v != d[v])
            continue;

        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                d[to] = d[v] + len;
                p[to] = v;
                q.push({d[to], to});
            }
        }
    }
}
```

-> getting rid of pairs in set implementation can improve the performance but then u will have to overload comparision operator of set such that it compares two vertices using the distances stored in d[].


**OBSERVATIONS:**
---

->Actually we can go without sorting the queue but then it won't be be dijkstra's and then it will exhaustively search for all the edges and all possible improvements and nodes will get pushed then popped multiple times so it won't be efficient either.\
-> Also not sure to what extent it is correct though haven't found any counter example yet\
-> ooo okay so if we use normal queue and push based on relaxations then it actually turns into spfa algorithm but it turns out that it doesn't have a good complexity because in worst case some node may get pushed n-1 times atmost 
