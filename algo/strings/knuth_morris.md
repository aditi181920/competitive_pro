**KMP AGO:**
--

-> Given string s of length n.\
-> Prefix function: array pie of length n, pie[i] = length of the longest proper prefix pf the substring s[0..i] which is not equal to the string itself.

-> Trivial algorithm is O(n^3)... (traversing(O(1)).. mapping every k sized substring till we can(O(n^2)))\
-> But every time we move 1 position forwards the value of the prefix function always either increases by 1, decreases by 1, stays same. Therefore we can redue this complexity to O(n^2)\
-> Second optimization is using the information computed in the previous steps. \

```cpp
vector<int> prefix_function(string s) {
    int n = (int)s.length();
    vector<int> pi(n);
    for (int i = 1; i < n; i++) {
        int j = pi[i-1];
        while (j > 0 && s[i] != s[j])
            j = pi[j-1];
        if (s[i] == s[j])
            j++;
        pi[i] = j;
    }
    return pi;
}

```

-> j++ things is obvious to get\
-> j=pi[j-1] thing is if current prefix does not match we need to look for smaller prefix with ends with some last characters of current last characters\
-> so we check for the the suffixes computed earlier .. but how does this gaurantee that this will be the longest suffix\
-> this is becoz j will give this first j characters of the prefix...so if it does not match we go to previous charcter and ask it what index of prefix did you match to go to next ? since it is a precomputed value it will give the largest possible answer ... then if that does not match either => okay this prefix is larger for the suffix as well => then we ask it which index to map from the next smaller prefix u got constructed from... and so on... ok this clearly works now\
-> if u observe carefully the jumps exactly do that ..\
-> they minimize the suffix to be matched with precomputed prefixes 


**Application:**
--

-> Find a given substring in a string \
-> substring+#+string \
-> now where ever prefix function value becomes n we know it appears there\
-> complexity: O(n+m)

