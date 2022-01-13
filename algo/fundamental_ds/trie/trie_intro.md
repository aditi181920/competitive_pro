**TRIE / PREFIX-TREE / NARY TREE / KEYWORD TREE:**
--

-> Rooted tree typically used to store strings (can also store number or keys though). \
-> each string starts at the root and each edge in the tree represents a single character ([or bit/digit)

**STRUCTURE:**
--

-> Each trie node represents a string (a prefix).\
-> Words that share the same prefix will also share some trie edges and nodes.
![image](https://user-images.githubusercontent.com/94597499/149326296-c7d63c24-e5de-4638-894d-5344af5c1027.png)

-> Root node is associated with the empty string.\
-> All descendants of a node have a common prefix of the string associated with that node. That's why Trie is also called prefix tree.\
-> To store words in the created trie tree we can mark end of a word in the trie by coloring the respective node. 

-> for example: a trie storing words - candle, canary, and can:
![image](https://user-images.githubusercontent.com/94597499/149327049-ea49db26-74a4-4a6b-b734-516146241dee.png)

-> If we add a word that doesn't share any prefix with the words already in the trie, we will have a new branch from the root node.
-> Example: adding lion in the previous example-
![image](https://user-images.githubusercontent.com/94597499/149327251-91ed4408-379e-4f6c-9e2a-dcb6cd98f8ea.png)

**IMPLEMENTATION:**
--

-> **INSERTION:**
--
-> When we insert a target value into a Trie, we will also decide which path to go depending on the target value we insert.\
-> If we insert a string s into Trie, we start with the root node and we will choose a child or a new child node depending on s[0], the first char in s.\
-> Then we go down to the second node and we will make a chioce according to s[1] aand we go down to the third node, so on and so for.\
-> Finally we traverse all characters in S sequentially and reach the end. The end node will be the node which represents the string s.

-> **SEARCH:**
--
-> Again we go down the tree depending on the given prefix. \
-> Once we cannot find the child node we want, search fails.\
-> If we reach a node which gives a prefix equal to the search string and that node is marked as a valid word the search succeeds.

-> **COMPLEXITY:**\
-> **time:** O(length of string) for both insertion and deletion\
-> **memory:** if large number of common prefixes then a large number of memory may be saved but in worst case there can be no memory optimization

**Example 2d array implemetation of trie:**
```cpp
let f be the matrix representation of your trie

let f[k] be the list of links for the k-th node

let f[k][x] = m, the node who represents the son of k-th node using x-th character, m = -1 is there is not a link.

int MAX = Max number of nodes
int CHARSET = alphabet size
int ROOT = 0
int sz = 1;

f[MAX][CHARSET]

void init() {
 fill(f, -1);
}

void insert(char [] s) {
 int node = ROOT;
 for (int i = 0; i < size(s); i++) {
   if ( f[node][ s[i] ] == -1 )
      f[node][ s[i] ] = sz++;
   node = f[node][ s[i] ];
 }
}
Notes: Root node is at f[0] sz is the numbers of nodes currently in trie
```
