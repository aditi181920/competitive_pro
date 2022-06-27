**DETECTING CYCLE IN A GRAPH:**
--
**1. Using dfs **

If we visit a node again in current ongoing depth then there exists a cycle but if we visit visited nodes through different depths then that does not indicate cycle
```cpp
int cyc=0;
void dfs(vector<vector<int>> &g,vector<int> &visited,int node){
    visited[node]=2;  
    for(auto x:g[node]){  
        if(visited[x]==2){
            cyc=1;
            return;
        }else if(!visited[x])dfs(g,visited,x);
    }
    visited[node]=1;
}
```

**2. FLOYD'S/TORTOISE AND HARE:**
--

In this algo we suppose that hare moves 2 steps at a time and tortoise moves only 1 step at a time. If there is a cycle then there will be a point where these 2 meet.

CONSTRUCTING CYCLE:
--
We can construct a cycle such as we first detect cycle then the we take the ndoe which ensures the presence of the cycle as the start of the cycle\
From there we can create a path which keep the nodes which have not been exited yet in the sequence in which they were entered and when we encounter the starting node again our cycle is complete

```cpp
int done=0;
void dfscyc(vector<vector<int>> &g,vector<int> &visited,int node){
    if(done==1)return;
    visited[node]=1;
    path.push_back(node);
    for(auto x:g[node]){
        if(x==cycnode){
            done=1;
            return;
        }
        if(!visited[x]){
            dfscyc(g,visited,x);
        }
    }
    if(done==0)path.pop_back();
}
```

This constructs any one cycle of all the cycles present in the graph
