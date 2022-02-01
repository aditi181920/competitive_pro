**SUM OF SUBSET:**
--

**NAIVE ALGORITHM:**
```cpp
	bool dp[range];   //initialize all to 0
	dp[0]=1;
	tot=0;
	vector<int> v(n); // vector of elements
	for(int i=0; i<n; i++){
	    for(int j=tot;j>=0; j--){
	        if(dp[j]){                        //if this sum is valid the adding any other element to the sum is also valid
	            dp[j+v[i]]=1;                 //can add additional constraint here if j+v[i] exceeds array bounds
	        }
	    }
	tot+=v[i];
	}
//now the sums obtainable will have true dp values and sum not obtainable will have false dp values
COMPLEXITY: O(n*n*x)    (n*x is the bound of sum of elements)   
```

**SOLVING SOS DP USING BITMASKS:**
--

Given a fixed array A of 2^n integers, we need to calculate for every x, f(x) = sum of all A[i] such that x&i = i, i.e., i is a subset of x
   f[mask] = summation(i is a subset of mask) A[i] 
   
**BRUTEFORCE:**

```cpp
for(int mask=0;mask<(1<<n);++mask){
    for(int i=0;i<(1<<n);++i){
        if((mask&i)==i){      //if i is a subset of given mask
            f[mask]+=a[i];
        }
    }
}
Complexity : O(4^n)
```

**SUBOPTIMAL SOLUTION:**

```cpp
We know we can iterate over submasks of masks in O(3^n) complexity
for(int mask = 0 ; mask < (1<<n); mask++){
    f[mask]=a[0];
    for(int mask;i>0;i=(i-1)&mask){
        f[mask] += a[i];
    }
}
Complexity analysis: We can analyse the time complexity in 2 ways-
  1. every bit has 3 choices based on inclusion in m and s so 3^n total iterations
  2. total number of iterations will be equal to total number of possible submask generated 
   --> we can find this using combinations 
   --> total number of submask generated = for every length i summation( possible mask having i enabled bits * total submask of a mask having i enabled bits)
   --> summation k=0 to n(( n choose k)(2^k))
   --> using binomial theorem this reduces to (1+2)^n => 3^n
```

**MORE OPTIMAL SOLUTION:**
--

-> Flaw in previous approach:\
-> an index A[x] with x having k off bits is visited by 2^k masks thus leading to repeated calculation (say we have 10100- 3 off bits here all the states here are visited by 10110 since submasks of 10100 are all submasks of 10110 as well similarly all k off bits offer choice to construct a supermask which constitutes the submask completely leading to repeated calculation)\

-> we can somehow make this non intersecting :\
```sh
  S(mask) = {x|x is a subset of mask} === can change this thing to ===> S(mask,i) = {x|x is a subset of mask and mask xor x < 2^(i+1)} 
  that is the set of only those subsets of mask which differ from mask only in the first i bits (zero based)
  for ex: S(1011010,3) = {1011010,1010010,1011000,1010000}
  
  TRANSITIONS:
  S(mask,i) = contains all subsets of mask which differ from it only in the first i bits
  Consider that ith bit of mask is 0 . Wr can't have a submask having this bit as 1 so no subset can differ from mask in the ith bit 
    => S(mask,i) = S(mask, i-1)  given ith bit in mask is off
  if ith bit of mask is 1 then the numbers belonging to S(mask,i) can be divided into two non intersecting sets
  -> ith bit 1 and differing from mask in the next i-1 bits
  -> ith bit 0 and differing from mask in the next i-1 bits 
  
```



-> these relations form a directed acyclic graph and not necessarily a rooted tree ( think abt diff values of mask and same value of i)

**ITERATIVE VERSION:**

```cpp
    for(int mask = 0; mask < (1<<N); ++mask){
	     dp[mask][-1] = A[mask];	//handle base case separately (leaf states)
	     for(int i = 0;i < N; ++i){
		       if(mask & (1<<i))
			         dp[mask][i] = dp[mask][i-1] + dp[mask^(1<<i)][i-1];
		       else
			         dp[mask][i] = dp[mask][i-1];
	     }
	     F[mask] = dp[mask][N-1];
    }
```
```cpp
//memory optimized, super easy to code.
for(int i = 0; i<(1<<N); ++i)
	F[i] = A[i];
for(int i = 0;i < N; ++i) for(int mask = 0; mask < (1<<N); ++mask){
	if(mask & (1<<i))
		F[mask] += F[mask^(1<<i)];
}
```
COMPLEXITY: O(n.2^n)
  

**SUBSET SUM SQ. ROOT OPTIMIZATION:**
--

1. **CLASSICAL SOS DP PROBLEM (discussed above):**

-> we can solve the classical dp problem in O(n*n*x) (the sum of elements is bounded by n*x)\
-> in that we created an dp array of size x+1 and said that dp<sub>a</sub> is 1 if it is possible to form a sum of a using some elements from the array and 0 otherwise.\
-> for that we try to include every element A<sub>i</sub> and set all dp<sub>a</sub> for which dp<sub>a-A<sub>i</sub></sub> is 1, to 1\

-> however if the sum of elements is bounded by n, it turns out that this problem can be solved in O(n*sqrt(n)). Formally, we have the following constraint  1<= summation(i=1 to n) Ai <= n\
-> what is the max no. of distinct elements our array can have if its sum is bounded by n?\
-> since maximizing no. of elements we must take as many small elements as possible\
-> so we wanna find smallest p s.t sum of first p natural naumbers is equal to n\
```sh
  (p(p+1))/2 = n  =>  p=sqrt(2*n-p)
                  => p=sqrt(2*n) (approx)
  so we can have atmost sqrt(2*n) distinct values in the array, which allows to develop an O(n*sqrt(n)) algorithm
```
-> defining dp:
```sh
   definition of dp is the same only transitions change
   we can process elements in pair
   (wi, ki) : wi = value of element i of compressed array, ki = frequency of element i of compressed array
   how to update dp array ?
  
  Let's take a look at what an array (0,1,2,3,4,5,6,7,8....) looks like if the ith element is i%wi. 
  Consider wi=4:   [0,1,2,3,0,1,2,3,0,1,2,...]
  So, for each Wi, let T be any value smaller than Wi and greater than or equal to 0 (0<=T<=Wi-1)
  Array indices with same value of T are exactly Wi elements apart
  ith index of dp stores if we can form a sum i
  since the same T values occur Wi elements apart, going from one occurence of T to the next uses a single copy of Wi.
  since we can have exactly ki copies of wi, we can form sum i if dp[i-Wi*y] for some y(0<=y<=ki) is one.
  so if sum of all such dp values is positive (atleast 1 has value 1), then dpi is possible.
  we can maintain a variable which stores the sum of the last ki such dp values .
  for example: 
  if wi=4 and lets look at indices where t=1 we have elements [1,5,9]
  then for ninth index, if we have atleast two copies of wi=4, then we want atleast one of dp[5],dp[1] to be 1
```
-> complexity:
```sh
  for every wi, for every index p in the range [0,wi-1], we loop over all multiples of wi starting at p.
  that is a total of n/wi multiples per p. 
  since p assumes exactly wi different values, complexity for doing so is O(wi * (n/wi)). 
  since we have sqrt(2*n) different values of wi then final complexity of O(n*sqrt(n))
```

**IMPLEMENTATION:**

```cpp
#include <bits/stdc++.h>
using namespace std;
int main() {
    int N;
    cin >> N;
    // Sum of elements <= N implies that every element is <= N
    vector<int> freq(N + 1, 0);
    for (int i = 0; i < N; i++) {
        int x;
        cin >> x;
        freq[x]++;
    }
    vector<pair<int, int>> compressed;
    for (int i = 1; i <= N; i++) {
        if (freq[i] > 0) compressed.emplace_back(i, freq[i]);
    }
    vector<int> dp(N + 1, 0);
    dp[0] = 1;
    for (const auto &[w, k] : compressed) {
        vector<int> ndp = dp;
        for (int p = 0; p < w; p++) {
            int sum = 0;
            for (int multiple = p, count = 0; multiple <= N; multiple += w, count++) {
                if (count > k) {
                    sum -= dp[multiple - w * count];
                    count--;
                }
                if (sum > 0) ndp[multiple] = 1;
                sum += dp[multiple];
            }
        }
        swap(dp, ndp);
    }
    cout << "Possible subset sums are:\n";
    for (int i = 0; i <= N; i++) {
        if (dp[i] > 0) cout << i << " ";
    }
}
```
**PROBLEM LINK:**
--
[BETA RD 77 DIV1 E](https://codeforces.com/contest/95/problem/E)
