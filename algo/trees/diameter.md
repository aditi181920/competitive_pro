**DIAMETER OF A TREE:**
--

Diameter of a tree is the length of the longest path between any nodes in the tree.

**Method 1:**
-
-> Choose any arbitrary node and do dfs\
-> The farthest node must be one end of diameter\
-> Pick the farthest node and do dfs again now the largest path obtained is the diameter\

*Proof:*
--
We can prove this by contradiction\

-> Let's say that s is arbitrary node and d is the farthest node\
-> Let's say diameter is not present in the subtree of s where d is present\
-> But since d is the farthest from s obviously replacing one end of diameter with d will be greater which is a contradiction



**Method 2:**
-
-> Choose any arbitrary node as root of the tree\
-> Now if the root does not pass through the diamt => any one of its children contain the diamt\
-> so algo becomes:
1. Go down the subtree everytime
2. When we come back then
3. dia=max(dia,dp[child1]+dp[child2]+1) .. where dp[] is depth
So we can compute diameter by considering every node as passing through diameter 


--> Implementation for this is ez
