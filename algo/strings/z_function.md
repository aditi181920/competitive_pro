**Z function:**
--

z[i] = length of longest string that is at the same time, a prefix of s and a prefix of the suffix of s starting at i\
z[0] is generally not well defined- we can assume it zero
(isn't this same def in KMP? ok KMP is a bit different it is longest suffix ending at i which is prefix and z function is longest suffix starting at i which is prefix)
Example:\
"aaabaab": [0,2,1,0,2,1,0]

-> so how this algo works is we define z blocks ... now let's say we got a matching with first character if it matches then match next with second.. so goes on until u can keep on matching and that forms a z block\
-> so now the since this block matches with the prefix.. and we have already computed the values for the prefix so we can copy every next character in this block with the precomputed values\
-> there is one catch though\
-> if the value exceeds the block size or just touches it .. we don't know about things outside block so for that we can limit the value till the boundary and we can continue checking further on their turns 

```cpp
vector<int> z_function(string s) {
    int n = (int) s.length();
    vector<int> z(n);
    for (int i = 1, l = 0, r = 0; i < n; ++i) {
        if (i <= r)
            z[i] = min (r - i + 1, z[i - l]);
        while (i + z[i] < n && s[z[i]] == s[i + z[i]])
            ++z[i];
        if (i + z[i] - 1 > r)
            l = i, r = i + z[i] - 1;
    }
    return z;
}

```
