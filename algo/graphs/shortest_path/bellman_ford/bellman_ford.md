**SINGLE SOURCE SHORTEST PATH WITH BOTH POSITIVE / NEGATIVE WEIGHT EDGES:**
--

-> COMPLEXITY: O(nm)\
-> sssp\
-> can't be used on graph containing cycles\
-> can be used with negative weight edges\
-> but it won't give shortest path in case of negative weight cycle\
-> but this algo can signal the presence of a cycle of negative wt/deduce this cycle

**1. ALGO:**
---

-> Assuming the graph contains no negative weight cycle. \
-> d[0...n-1] : array of shortest distances from source to respective vertices\
-> initially, d[s]=0 and all other d[] = inf\
-> at each iteration all edges of the graph, the algo tries to produce relaxation along each edge (a,b) having weight c\
-> relaxation: improving d[b] using d[a] + c \
-> claim: n-1 phases of the algorithm are sufficient to correctly calculate the lengths of all shortest paths in the graph\
-> for unreachable vertex : d[] will remain inf

**2. PROOF:**
---

-> After ith phase execution, the algo correctly finds all shortest paths whose number of edges does not exceed i\
-> For any vertex a if k number of edges is in the shortest path to it, the algo guarantees that after kth phase shortest path for vertex a will be found\
-> starting vertex v and ending vertex a ... path goes like (po=v, p1,...,pk=a). \
-> Before 1st phase , po=v was found correctly then during 1st phase edge (po,p1) has been checked by the algorithm and then the distance to the vertex p1 was correctly calculated after 1st phase.\
-> after kth phase distance to vertex pk=a gets calculated correctly\
-> algo shortest path cannot have more than n-1 edges so the algo sufficiently goes upto (n-1)th phase. After that it is guaranteed that no relaxation will improve the distance to some vertex.\
-> also the algo may end before n-1 phase we can know about that if some current phase does not do any relaxation then any subseq phase won;t either

**3. RETRIEVING PATH:**
---

-> again same way we update p[] if relaxation is performed 

**4. IMPLEMENTATION:**
---

```cpp
void solve()
{
    vector<int> d (n, INF);
    d[v] = 0;
    vector<int> p (n, -1);

    for (;;)
    {
        bool any = false;
        for (int j = 0; j < m; ++j)
            if (d[e[j].a] < INF)
                if (d[e[j].b] > d[e[j].a] + e[j].cost)
                {
                    d[e[j].b] = d[e[j].a] + e[j].cost;
                    p[e[j].b] = e[j].a;
                    any = true;
                }
        if (!any)  break;
    }

    if (d[t] == INF)
        cout << "No path from " << v << " to " << t << ".";
    else
    {
        vector<int> path;
        for (int cur = t; cur != -1; cur = p[cur])
            path.push_back (cur);
        reverse (path.begin(), path.end());

        cout << "Path from " << v << " to " << t << ": ";
        for (size_t i=0; i<path.size(); ++i)
            cout << path[i] << ' ';
    }
}
```

**5. PRESENCE OF NEGATIVE WEIGHT CYCLE:**
---

-> In case of presence of negative weight cycles you can go on relaxing its nodes indefinitely\
-> Distances to all vertices in this cycle as well as distances to vertices reachable from this cycle is not defined- they should be eq to minus infinity\
-> So after n-1 th phase if we run the algo for one more phase and it performs atleast one more relaxation, then the graph contains a negative weight cycle that is reachable from v\
-> now we can even retrieve this cycle:\
-> remember last vertex x from which there was a relaxation in nth phase.\
-> this vertex will either lie in the negative weight cycle or is reachable from it \
-> we have to find a vertex y which is guaranteed to lie in the negative cycle and to do so we start from the vertex x and pass through to the predecessors n times\
-> then we get the vertex y which is sure to lie in the negative weight cycle\
-> now we can go from this vertex to all the predecessors till we come back to y and all the nodes obtained will form negative weight cycle (relaxation in a negative weight cycle occurs in a circular manner)

**IMPLEMENTATION:**
--
```cpp
void solve()
{
    vector<int> d (n, INF);
    d[v] = 0;
    vector<int> p (n - 1);
    int x;
    for (int i=0; i<n; ++i)
    {
        x = -1;
        for (int j=0; j<m; ++j)
            if (d[e[j].a] < INF)
                if (d[e[j].b] > d[e[j].a] + e[j].cost)
                {
                    d[e[j].b] = max (-INF, d[e[j].a] + e[j].cost);   //handle underflows due to negative wt cycles
                    p[e[j].b] = e[j].a;
                    x = e[j].b;
                }
    }

    if (x == -1)
        cout << "No negative cycle from " << v;
    else
    {
        int y = x;
        for (int i=0; i<n; ++i)
            y = p[y];

        vector<int> path;
        for (int cur=y; ; cur=p[cur])
        {
            path.push_back (cur);
            if (cur == y && path.size() > 1)
                break;
        }
        reverse (path.begin(), path.end());

        cout << "Negative cycle: ";
        for (size_t i=0; i<path.size(); ++i)
            cout << path[i] << ' ';
    }
}
```
-> this algo can be modified  to look for any negative cycle in the graph\
-> if we set d[v] = 0 for all v then relaxations will only happen due to negative weight cycle and that's it \
-> so in one iteration we can find the vertices that are either in negative weight cycles or reachable from it then we can find those lying in the negative weight cycles in similar way

