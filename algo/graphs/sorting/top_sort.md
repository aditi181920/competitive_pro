**TOPOLOGICAL SORT:**
--

If for every vertex (u,v) such that there is an edge from u to v, u appears before v in the sorted sequence then the sequence is the topological sort.\
It is not unique.\
It may not exist at all if graph contains cycle.

**1. Using dfs**

If we construct a path such that if u appears before v such that u exists before v does in the dfs graph traversal then we obtain an topologically sorted array
```cpp
int n; // number of vertices
vector<vector<int>> adj; // adjacency list of graph
vector<bool> visited;
vector<int> ans;

void dfs(int v) {
    visited[v] = true;
    for (int u : adj[v]) {
        if (!visited[u])
            dfs(u);
    }
    ans.push_back(v);
}

void topological_sort() {
    visited.assign(n, false);
    ans.clear();
    for (int i = 0; i < n; ++i) {
        if (!visited[i])
            dfs(i);
    }
    reverse(ans.begin(), ans.end());
}
```

**2. Using in-degree:**

The node having zero in-degree must always be the one to be visited first. If there is no such node then it is ambiguous to decide which node comes first.\
So the algorithm goes like:
1. push all node which indegree 0 in the queue
2. then start taking nodes from queue top
3. remove the edges outgoing from these nodes 
4. if new nodes with incoming edges are obtained then push them in the queue

```cpp
#define rep(i,n) for (int i=0;i<(int)(n);++i)
#define sz(x) (int)(x).size()
vector<int> topoSort(const vector<vi>& gr) {
	vector<int> indeg(sz(gr)), ret;
	for (auto& li : gr) for (int x : li) indeg[x]++;
	queue<int> q; // use priority_queue for lexic. largest ans.
	rep(i,sz(gr)) if (indeg[i] == 0) q.push(i);
	while (!q.empty()) {
		int i = q.front(); // top() for priority queue
		ret.push_back(i);
		q.pop();
		for (int x : gr[i])
			if (--indeg[x] == 0) q.push(x);
	}
	return ret;
}
```
