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
let triee be the matrix representation of your trie
let triee[i] be the list of links for the k-th node
let triee[i][x] = m, the node who represents the son of ith node using x-th character, m = 0 is there is not a link.

#define ll long long int
ll triee[1000000][26];
class Trie {
public:
    ll tot;
    map<ll,int> mark;
    Trie() {
        tot=2;
        memset(triee,0,sizeof(triee));
    }
    void insert(string word) {
        int node=1;
        for(int i=0;i<word.size();i++){
            int d=word[i]-'a';
            if(triee[node][d]==0){
                triee[node][d]=tot;   //inserting new node
                tot++;
            }
            node=triee[node][d];   //going down the path
        }
        mark[node]=1;
    }
    bool search(string word) {
        int node=1;
        for(int i=0;i<word.size();i++){
            int d=word[i]-'a';
            if(triee[node][d]==0){
                return false;
            }
            node=triee[node][d];
        }
        if(mark[node]==1){
            return true;
        }
        else return false;
    }
    bool startsWith(string prefix) {
        int node=1;
        for(int i=0;i<prefix.size();i++){
            int d=prefix[i]-'a';
            if(triee[node][d]==0){
                return false;
            }
            node=triee[node][d];
        }
        return true;
    }
};
```
**Example pointers inmplementation of trie:**
```cpp
#define ll long long int
struct node{
    ll freq;
    node* child[26];
    bool valid;
};
node *getnode(){
    node* n=new node();
    for(int i=0;i<26;i++){
        n->child[i]=NULL;
    }
    n->valid=false;
    n->freq=0;
    return n;
}
class Trie {
public:
    map<ll,int> mark;
    node *root;
    Trie() {
        root = getnode();
    }
    
    void insert(string word) {
        node *temp=root;
        root->freq++;
        for(int i=0;i<word.size();i++){
            int d=word[i]-'a';
            if(temp->child[d]==NULL){
                temp->child[d]=getnode();
            }
            temp=temp->child[d];
            temp->freq++;
        }
        temp->valid=true;
    }
    
    bool search(string word) {
        node *temp=root;
        for(int i=0;i<word.size();i++){
            int d=word[i]-'a';
            if(temp->child[d]==NULL){
                return false;
            }
            temp=temp->child[d];
        }
        if(temp->valid==true){
            return true;
        }
        else return false;
    }
    
    bool startsWith(string prefix) {
        node *temp=root;
        for(int i=0;i<prefix.size();i++){
            int d=prefix[i]-'a';
            if(temp->child[d]==NULL){
                return false;
            }
            temp=temp->child[d];
        }
        return true;
    }
};
```
