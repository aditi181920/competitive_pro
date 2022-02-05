**BINARY UPLIFTING:**
---

**ALGORITHM:**
---

-> up[i][j]= 2^j-th ancestor above the node i with i=1....N,j=0...ceil(log(N))[this info allows to jump from any node to any ancestor above it in O(logn) time]\
-> we can compute this array using a DFS traversal of the tree.\
-> keep info abt time of first visit of the node and the time when we left it, this info can be used to determine if a node is an ancestor of another node\
-> if we recieve query (u,v) we can check whether one node is the ancestor of the other, if yes then this node is already the LCA.\
-> else climb the ancestors of u until we find the highest node which is not an ancestor of v\

-> let l=ceil(log(n))\
-> suppose first that i=l, if up[u][i] is not an ancestor of v, then we can assign u=up[u][i] and decrement i\
-> if up[u][i] is an ancestor then just decrement i\
-> clearly doing this for all non-negative i the node u will be desired node- i.e. u is still not an ancestor of v, but up[u][0] is\
-> answer to LCA will be up[u][0]-i.e. the smallest node among the ancestors of the node u, which is also an ancestor of v\
-> So answering LCA query will iterate i from ceil(log(n)) to 0 and checks in each iteration if one node is the ancestor of the other\
-> each query can be answered in O(logn)

**IMPLEMENTATION:**
```cpp
int n, l;
vector<vector<int>> adj;

int timer;
vector<int> tin, tout;
vector<vector<int>> up;

void dfs(int v, int p)
{
    tin[v] = ++timer;
    up[v][0] = p;
    for (int i = 1; i <= l; ++i)
        up[v][i] = up[up[v][i-1]][i-1];

    for (int u : adj[v]) {
        if (u != p)
            dfs(u, v);
    }

    tout[v] = ++timer;
}

bool is_ancestor(int u, int v)
{
    return tin[u] <= tin[v] && tout[u] >= tout[v];
}

int lca(int u, int v)
{
    if (is_ancestor(u, v))
        return u;
    if (is_ancestor(v, u))
        return v;
    for (int i = l; i >= 0; --i) {
        if (!is_ancestor(up[u][i], v))
            u = up[u][i];
    }
    return up[u][0];
}

void preprocess(int root) {
    tin.resize(n);
    tout.resize(n);
    timer = 0;
    l = ceil(log2(n));
    up.assign(n, vector<int>(l + 1));
    dfs(root, root);
}
```
**COMPLEXITY:**
---
-> Preprocessing: O(nlogn)\
-> LCA query: O(logn)



