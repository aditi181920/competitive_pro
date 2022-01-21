** Given an array of +ve integers you have to print the number of subarrays whose XOR is less than k**

-> for each index i=1 to N, we can count how many subarrays ending at ith position satisy the given condition.
```cpp
ans=0 
p=0 
for i=1 to N: 
    q=p XOR A[i] 
    ans += Trie.query(q,k) 
    Trie.insert(q) 
    p=q 
```
-> query(q,k) returns how many integers already exist into structure which when taken xor with q returns an integer less than k\
-> we compare the corresponding bits of p and q, beginning from msb \
-> suppose p and q are respective bits we are considering now: \
-> then we can make cases for (q=1,p=1),(q=0,p=1),(q=1,p=0),(q=0,p=0)\
-> also we need to keep the number of leaf nodes reachable from current node if i go to the right and left so we won't have to traverse the whole tree again and again thus reducing the complexity

-> Some example implementation:
```sh
insert(root, num, level): 
    if level==-1: return root 
    x=level'th bit of num 
    if x==1: 
        if root->right is NULL: create root->right 
        else: insert(root->right,num,level-1) 
    else: 
        if root->left is NULL: create root->left 
        else: insert(root->left,num,level-1) 
```

**PROBLEM LINK:** [SPOJ](https://www.spoj.com/problems/SUBXOR/)
