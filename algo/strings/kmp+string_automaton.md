**STRING AUTOMATON**
--

-> This is a DFA using which we can generate prefix value of next character c added to string in const time rather than using kmp again and getting linear time\
-> This way if we do n additions we complete it in O(n)\*(alphabet size) complexity rather than O(n^2)\*(alphabet size)  complexity

-> it is same as just building a dfa. While building this dfs if the next character added is the chracter of the string then we go to the next state else we find the longest prefix which is a suffix and jump there accordingly 


-> Given string abbaba, then its dfa must be:
![image](https://user-images.githubusercontent.com/94597499/187903136-566e45d2-44c8-46b7-8a6e-f867cf7fccda.png)


-> Now the trivial algorithm for building this automaton is just:

```cpp
void compute_automaton(string s, vector<vector<int>>& aut) {
    s += '#';
    int n = s.size();
    vector<int> pi = prefix_function(s);
    aut.assign(n, vector<int>(26));
    for (int i = 0; i < n; i++) {
        for (int c = 0; c < 26; c++) {
            int j = i;
            while (j > 0 && 'a' + c != s[j])
                j = pi[j-1];   //find longest prefix such that it is suffix
            if ('a' + c == s[j])  //now if next character is same => we can follow transition to its next state else just go there
                j++;
            aut[i][c] = j;
        }
    }
}
Complexity : O(n^2 * |alphabet|)
```

-> Note that if we want to find aut[i+1][c] and we know aut[i][c] then it is easy to find.. if next character is req then go ahead else whereever the we get longest i-1 prefix such that it is suffix then transitioning by req character there will give us longest i prefix such that it is suffix 

```cpp
void compute_automaton(string s, vector<vector<int>>& aut) {
    s += '#';
    int n = s.size();
    vector<int> pi = prefix_function(s);
    aut.assign(n, vector<int>(26));
    for (int i = 0; i < n; i++) {
        for (int c = 0; c < 26; c++) {
            if (i > 0 && 'a' + c != s[i])
                aut[i][c] = aut[pi[i-1]][c];
            else
                aut[i][c] = i + ('a' + c == s[i]);
        }
    }
}

Complexity: O(n*|alphabet|)

```

Note: We can find kmp separately in this problem and then do this string automaton separately and it will do the job but we can smartly do kmp here as well\
Notice the similarity in kmp and building this automaton, it is the same property -> finding longest prefix such that it is the suffix \
-> Now abuse this property to calculate kmp using dfa as well

```cpp

void compute_automaton(string s, vector<vector<int>>& aut) {
    s += '#';
    int n = s.size();
    vector<int> pi ;
    aut.assign(n, vector<int>(26));
    for (int i = 0; i < n; i++) {
        pi[i+1]=aut[pi[i],s[i]);
        for (int c = 0; c < 26; c++) {
            if (i > 0 && 'a' + c != s[i])
                aut[i][c] = aut[pi[i-1]][c];
            else
                aut[i][c] = i + ('a' + c == s[i]);
        }
    }
}

Complexity: O(n*|alphabet|)
```

**PROBLEM LINKS:**
--

[EDU 134 DIV 2](https://codeforces.com/contest/1721/problem/E)
