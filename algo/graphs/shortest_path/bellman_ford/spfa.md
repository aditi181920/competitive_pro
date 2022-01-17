**SHORTEST PATH FASTER ALGORITHM (SPFA):**
--

-> improvement of Bellman-Ford algorithm\
-> it is also said that is is a combination of bfs+dijkstra\
-> Idea: Not all attempts at relaxation works so we create a queue containing only the vertices that were relaxed but that still could further relax their neighbours\
-> Whenever you relax a neighbour put him in the queue\
-> This algo can be used to detect negative cycles as the Bellman - Ford
-> Though the worst case is O(mn) but in practice it runs much faster\
-> this algo can continue forever if there is some presence of negative weight cycles \
-> for this we can keep a counter for the number of times the vertex has been relaxed , if relaxed for the nth time them no need to put it back in the queue\

**IMPLEMENTATION:**
---

```cpp
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

bool spfa(int s, vector<int>& d) {
    int n = adj.size();
    d.assign(n, INF);
    vector<int> cnt(n, 0);
    vector<bool> inqueue(n, false);
    queue<int> q;

    d[s] = 0;
    q.push(s);
    inqueue[s] = true;
    while (!q.empty()) {
        int v = q.front();
        q.pop();
        inqueue[v] = false;

        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                d[to] = d[v] + len;
                if (!inqueue[to]) {
                    q.push(to);
                    inqueue[to] = true;
                    cnt[to]++;
                    if (cnt[to] > n)
                        return false;  // negative cycle
                }
            }
        }
    }
    return true;
}
```
