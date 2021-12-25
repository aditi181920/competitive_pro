BINARY SEARCH:
---
COMPLEXITY: O(LOG2N)+2

   **PREREQUISITE**  \
   -> on a sorted container defined explicitly\
   -> on a sorted sequence defined implicitly/ assumed
   
   STD B.SEARCH TO FIND IF A KEY EXISTS IN AN ARRAY:
   ```cpp
   bool bsearch(int x[], int n, int k) {
    int l = 0, r = n-1;
    while (l <= r) {
        int m = (l+r)/2;
        if (x[m] == k) return true;
        if (x[m] < k) l = m+1; 
        else r = m-1;
        }
    return false;
    }
   ```
   Note: often while binary search we may encounter bugs regarding stopping condition\
   One of the useful trick to remove such kind of bugs is that: \
   -> instead of stopping when l==r , we can stop earlier when l is just a little behind r\
   -> then we can just brute force check for the remaining values
   
   
   SOME ALTERNATIVE BINARY SEARCH IMPLEMENTATIONS:
   ```cpp
   //searching for an element in an array
   bool search(int x[], int n, int k) {
    int p = 0;
    for (int a = n; a >= 1; a /= 2) {
        while (p+a < n && x[p+a] <= k) p += a;
     }
    return x[p] == k;
    }
   
   //searching for freq of an element in array
   int count(int x[], int n, int k) {
    int p = -1, q = -1;
    for (int a = n; a >= 1; a /= 2) {
        while (p+a < n && x[p+a] < k) p += a;
        while (q+a < n && x[q+a] <= k) q += a;
        }
    return q-p;
    }
   ```
    
PROBLEM LINKS:\
[Codeforces 762 div 3  D](https://codeforces.com/contest/1619/problem/D)
