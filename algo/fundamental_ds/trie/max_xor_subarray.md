**Given an array of integers, find the subarray with max XOR**

-> Let's say f(l,r) is the XOR of subarray from l or r\
-> f(l,r) = f(1,r) xor f(1,l-1) [ since duplicate terms will eventually become zero by prop of xor ]\
-> now lets say we have found xor till r. We need to find some l s.t. f(1,r) xor f(1,l) is max\
-> we can maintain a trie and for every r insert the f(1,r) in trie and find some f(1,l)\
-> [ACM-ICPC Live Archive](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&category=345&page=show_problem&problem=2683)


**IMPLEMENTATION:**

```cpp
ans=0 
pre=0 
Trie.insert(0) 
for i=1 to N: 
    pre = pre XOR a[i] 
    Trie.insert(pre) 
    ans=max(ans, Trie.query(pre)) 
print ans 
```


