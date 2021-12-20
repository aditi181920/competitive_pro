TEMPLATE:
```sh
struct dsu{
    vector<int> p,s;
    dsu(int n){
        p.resize(n+1);
        iota(p.begin(),p.end(),0);
        s.resize(n+1,1);
        rank.resize(n+1,0);
    }
    int find_set(int x){              //Complexity: O(logn)
        if(p[x]==x){
            return x;
        }
        return p[x]=find_set(p[x]);  //path compression technique:
                                  //which sets the parent of all nodes in the path directly to representative of the set
                                  //worst case og O(n) is eliminated
    } 
    void union_set(int a,int b){    //union by size/rank(size of tree)
        a= find_set(a);
        b= find_set(b);
        if(a!=b){
            if(s[a]<s[b]){
                swap(a,b);
            }
            p[b]=a;
            s[a]+=s[b];     //attaching lower rank tree to bigger one
        }
    }
    	void union_sets(int a, int b) {   //union by size/rank(depth of tree)
	    a = find_set(a);
	    b = find_set(b);
	    if (a != b) {
	        if (rank[a] < rank[b])
	            swap(a, b);
	        parent[b] = a;
	        if (rank[a] == rank[b])
	            rank[a]++;          //since joining same depth tree will increase depth of main tree by 1
	    }
};
```


Linking by index / coin-flip linking\
	-> randomized algorithm\
	-> We assign each set a random value called the index, and we attach the set with the smaller index to the one with the larger one. \
  -> It is likely that a bigger set will have a bigger index than the smaller set, therefore this operation is closely related to union by size.\
  -> In fact it can be proven, that this operation has the same time complexity as union by size but in practice slightly slower.
	
```sh
  void make_set(int v) {
	    parent[v] = v;
	    index[v] = rand();
	}
	void union_sets(int a, int b) {
	    a = find_set(a);
	    b = find_set(b);
	    if (a != b) {
	        if (index[a] < index[b])
	            swap(a, b);
	        parent[b] = a;
	    }
	}

	-> but coin flipping performs a lot worse than union by size/rank or linking by index
	void union_sets(int a, int b) {
	    a = find_set(a);
	    b = find_set(b);
	    if (a != b) {
	        if (rand() % 2)
	            swap(a, b);
	        parent[b] = a;
	    }
	}
	
```

PROBLEM LINKS:\
[LEETCODE WEEKLY 269 PROBLEM D](https://leetcode.com/contest/weekly-contest-269/problems/find-all-people-with-secret/)\
[CODEFORCES DETLIX AUTUMN 2021 PROBLEM D](https://codeforces.com/contest/1609/problem/D)\

