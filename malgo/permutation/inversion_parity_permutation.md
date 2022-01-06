**BASIC'S**
--

Parity of permutation p is parity of number of inversions in it. \
Inversion is pair (i,j) s.t. i<j, pi>pj\
Composition of permutations is defined as: (f o g)x = f(g(x))\
Cyclic permutation: some indices are cyclic shifted, ex: p = (1 5 2 4 3) has a cycle (2 3 5)
  

  
  **THEOREM:** Every permutation is composition of non-intersecting cycles \
  **PROOF:** Consider directed graph where vertices are numbered from 1 to n, and edges are i->pi for all i. Since p is 
  permutation, indegree and outdegree of each vertex is 1, hence our graph is collection of cycles.
    
 **LEMMA:** Applying a swap operation to permutation will change its parity\
 **PROOF:** Consider permutation \_\_\_a\_\_\_b\_\_\_ (say a> b) (we can generate a similar proof for a<b)\
 -> part 1: no.'s appearing before a\
 -> part 2: no.'s appearing after a and before b\
 -> part 3: no.'s appearing after b\
 -> x2: no. of no.'s less than b in part 2\
 -> y2: no. of no.'s greater than b and less than a in part 2\
 -> z2: no. of no.'s greater than b in part 2\
 -> x3: no. of no.'s less than b in part 3\
 -> y3: no. of no.'s greater than b and less than a in part 3\
 -> z3: no. of no.'s greater than a in part 3\
 observation: on swapping a and b the change in no. of inversions of whole permutation will be only due to change in no.'s of inversions of sub-array a\_\_\_b\
 -> before swap:\
 ----> no. of inversion count of 'a': n1 = x2+y2+x3+y3+1 ( 1 for (a,b) pair)\
 ----> no. of inversion count of 'b': m1 = x3\
 -> after swap:\
 ----> no. of inversion count of 'a': n2 = x3+y3\
 ----> no. of inversion count of 'b': m2 = x2+x3\
 ----> inversion cnt of all no.'s > a increases by 1 (since now a appears after them)\
 ----> inversion cnt of all no.'s > b decreases by 1 (since now b appears before them)\
 => total change in inversions: n2+m2-(n1+m1)+z2-(z2+y2) = -2y2 - 1 which is odd\
 => since change in inversion for each swap is an odd no. therefore parity will definitely change
 
 **FACT:** Parity of (f o g) is sum of parities of f and g\
 **PROOF:** Applying swap to permutation changes its parity, so if permutation f can be represented as k swaps, then parity of k is parity of f.\
 So if f can be represented as k swaps and g can be represented as m swaps then (f o g) can be represented as k+m swaps.\
 So parity of (f o g) is parity of k+m, sum of parities of f and g
 
 **COUNTING INVERSIONS, PARITY OF PERMUTATION:**
 --
 -> There are many ways to cnt no. of inversions in O(n log n) time\
 -> Below is a simple way to cnt parity of permutation, w/o directly counting no. of inversions.
   
 **THEOREM:** Permutation can be represented as composition of 3-cycles only if it is even\
 **PROOF:** 3-cycle is even, so composition of 3-cycles must be even now we need to prove any even permutation can be represented as 3-cycle\
 -> on ith iteration we assume, that first  i-1 elements of permutation are in place, and we will try to place i-th element.\
 -> if the ith element is not in place, then now in the current permutation it is on jth place, j>i.\
 -> let's do cycle n->j->i if j not eq. n, and if j=n, do n-1->j->i, so we won't corrupt first i-1 elements, and we will place the ith element\
 -> so we can fix first n-2 elements like this as for the remaining 2 elements we can no longer apply the 3-cycle so we are left with 2 possible situations:\
 -----> n-1 th and nth element are in place => we represented our permutation as 3-cycles so our permutation is even and we got a representation for it\
 -----> they are not in place, they are swapped. Because a 3-cycle is two swap so now being left with 1 single swap after applying some 3-cycles i.e. even swaps => our permutation is odd => can't be represented
   
 -> **IMPLEMENTATION:**
 --
 ```cpp
 bool parity(const vector<int> &p) {
    int n = p.size();
    if (n == 1) return false;
    vector<int> cur(n);
    vector<int> inv_cur(n);
    iota(cur.begin(), cur.end(), 0);
    iota(inv_cur.begin(), inv_cur.end(), 0);
    auto do_cycle = [&](int i, int j, int k) {
        int tmp = cur[k];
        cur[k] = cur[j];
        cur[j] = cur[i];
        cur[i] = tmp;

        inv_cur[cur[i]] = i;
        inv_cur[cur[j]] = j;
        inv_cur[cur[k]] = k;
    };
    for (int i = 0; i < n - 2; i++) {
        if (cur[i] != p[i]) {
            int j = inv_cur[p[i]];
            if (j != n - 1) {
                do_cycle(n - 1, j, i);
            } else {
                do_cycle(n - 2, j, i);
            }
        }
    }
    return cur[n - 1] != p[n - 1];
}

COMPLEXITY: O(n)
 ```
 

   
   1. Theorem: statement proven using 1 or more propositions\
   2. lemma: minor result whose purpose is to help prove a more substantial theorem - a step in the direction of proof\
   3. corollary: proposition that follows from or is appended to a theorem already proven\
   4. proposition: statement that is either true or false
