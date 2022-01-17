**DIAL'S ALGORITHM:**
---

-> Optimization of Dijkstra's \
-> We know that Dijkstra's algorithm runs in O((E+V)logV)\
-> But if weight of edges is bounded in a very small range [1:K] were K is very small ( good if it is < or aprrox to logV)\
-> Then we can divide our queue into K+1 buckets and push the edges into this buckets according new edge weight of new path length found\
-> since there are k+1 buckets and max wt. is K so every vertex pushed by some vertex will go into some bucket coming after and we can just keep traversing the buckets to find the next closest vertex and then again update \
-> just like dijkstra but we have to work with bucket of queues instead of a single bucket


**SOME RANDOM CODES:**
---

1. ** Pushing using the edge weight encountered:**

```cpp
 bfs[0].push(start);
	d[start] = 0;
	int pos = 0, num = 1; // I recommend to define a variable num - the number of vertexes that are in the queues
	while (num > 0)
	{
		while (bfs[pos % (k + 1)].empty())
		{
			++pos;
		}
		int u = bfs[pos % (k + 1)].front(); 
		bfs[pos % (k + 1)].pop();
		--num;
		if (used[u]) // used vertex can be in other queues
		{
			continue;
		}
		used[u] = true;
		for (pair<int, int> edge : g[u])
		{
			int cost = edge.first, w = edge.second;
			if (d[u] + cost < d[w])
			{
				d[w] = d[u] + cost;
				bfs[d[w] % (k + 1)].push(w);
				++num;
			}
		}
	}
```

2. **Pushing using total path length covered till now:**
```cpp
template<typename Graph>
vector<int> SmallDijkstra(Graph& graph, int src, int lim) {
  vector<vector<int>> qs(lim);
  vector<int> dist(graph.size(), -1);

  dist[src] = 0; qs[0].push_back(src);
  for (int d = 0, maxd = 0; d <= maxd; ++d) {
    for (auto& q = qs[d % lim]; q.size(); ) {
      int node = q.back(); q.pop_back();
      if (dist[node] != d) continue;
      for (auto [vec, cost] : graph[node]) {
        if (dist[vec] != -1 && dist[vec] <= d + cost) continue;
        dist[vec] = d + cost;
        qs[(d + cost) % lim].push_back(vec);
        maxd = max(maxd, d + cost);
      }
    }
  }
  return dist;
}
```
