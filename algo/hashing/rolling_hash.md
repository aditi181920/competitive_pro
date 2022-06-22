**POLYNOMIAL ROLLING HASH FUNCTION:**
--
![image](https://user-images.githubusercontent.com/94597499/175011158-bdb00ea6-7f69-4f79-9841-cff3613c3169.png)

**Search for duplicate strings in an array of strings:**
--
-> Given s strings si, max m characters\
-> Sorting the strings -> O(mnlogn) (O(nlogn) comp and each comparsion O(m))\
-> By using hashing comp is O(1) -> hashing comp-> O(mn+nlogn) time [mn for calculating hash and nlogn sort to grp eq hashes together]

**Computing hash for arbitrary segments:**
--

**1. Method 1**


![image](https://user-images.githubusercontent.com/94597499/175012062-e569aa6b-6a27-416b-b12a-eb8553563eae.png)

Multiplying by p<sup>i</sup> gives:
![image](https://user-images.githubusercontent.com/94597499/175012178-dc9c644c-5a51-4754-940e-71430a4ae184.png)
Therefore to compute hash of substring, we only need hash of prefixes. But using this way we need division by p^i. So we need to calculate modular multiplicative inverses (which we can precompute)

**2. Method 2:**

-> for comparing 2 substrings that begin with i and j and have the length len:
![image](https://user-images.githubusercontent.com/94597499/175013181-17596ecb-e001-41e3-b516-56c1b474497c.png)
![image](https://user-images.githubusercontent.com/94597499/175013207-f1be997c-027b-4fbb-bb24-756ca69782c6.png)
![image](https://user-images.githubusercontent.com/94597499/175013255-533273fe-c690-4502-9b34-7b09013df909.png)
Since RHS is equal for checking equality of the segments we only need to check:
![image](https://user-images.githubusercontent.com/94597499/175013421-64e58ec6-fc0c-4012-9c53-b88554a7251e.png)
Problem in this method is one seg of seq depends on the parameters of the seg of sequence 

Alternative way can be:
![image](https://user-images.githubusercontent.com/94597499/175013686-93e0c506-97a5-4ee2-a1db-ee5c92ea6e67.png)
![image](https://user-images.githubusercontent.com/94597499/175013712-3a5fdf43-f3d3-4970-b472-8d9b17ac8a16.png)
But here we need to calculative inverses 

Another alternative way is:

Let mxpow - max length of the compared segments\
Multiplying both sides by mxpow-i-len+1 in equation 1 and by mxpow-j-len+1 in equation 2

![image](https://user-images.githubusercontent.com/94597499/175014608-4f4e69c2-804f-473a-a1bd-866662359c9d.png)
![image](https://user-images.githubusercontent.com/94597499/175014658-5b2dc485-7540-457b-828f-49bf0c728dd1.png)

Using these approaches we can compare substring of length len with all substring of length len by equality.

**Comparision of greater/less in O(logn) time**
--
We can go binary search+hashing\
Using binary search find first non equal character and result\
Since hashing is O(1) (precomputed ) and bin search O(logn)

**What if character at a place is changed:**
--
In this case whole hashing is not required to be done again\
if ch1 at index i is changed to ch2 then \
```sh
hash_new = hash_old-p^i (ch1) + p^i(ch2)
```

