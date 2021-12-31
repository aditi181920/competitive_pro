SPARSE TABLE
--
-> can answer most range queries in O(logn)\
-> mostly used for range min/max queries with complexity O(1)\
-> can only be used on immutable arrays\
-> if in between queries any element in the array changes the complete sparse table has to be recomputed\
-> precomputation of sparse table is O(nlogn)

INTUITION:
---
-> Any non-negative no. can be uniquely represented as a sum of decreasing powers of two\
-> for a number x there can be atmost ceil(log2x) summands. e.g. 13 = (1101)2 = 8+4+1\
-> similarly any interval can be uniquely represented as a union of intervals with lengths that are decreasing powers of two\
-> the union consists of atmost ceil(log2(length of interval)) many intervals

**MAIN IDEA:**\
-> precompute all answers for range queries with power of two length. \
-> any range can then be answered by splitting it in largest power of two segment looking them up in table and combining the values back

PRECOMPUTATION:
---
-> st[i][j] : stores answer for range [i,i+2^(j) - 1] of length 2^j\
-> size of st : maxn x (k+1)  ; maxn = biggest possible array length, k>=floor(log2 (maxn))\
-> [i, i+2^j-1] of length 2^j splits into: [i,i+2^(j-1)-1] and [i+2^(j-1),i+2^j-1] both of length 2^(j-1)\
=> we can generate table efficiently using dp\
-> the function f will depend on the type of query
```cpp
int st[MAXN][K + 1];
for (int i = 0; i < N; i++)
    st[i][0] = f(array[i]);

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = f(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);
```
**COMPLEXITY:** O(nlogn)

RANGE SUM QUERIES:
---
-> f(x,y) = x+y
```cpp
long long st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = st[i][j-1] + st[i + (1 << (j - 1))][j - 1];
```
--> answering sum query for the range [l,r]:
```cpp
long long sum = 0;
for (int j = K; j >= 0; j--) {
    if ((1 << j) <= R - L + 1) {
        sum += st[L][j];
        L += 1 << j;
    }
}
```
**TIME COMPLEXITY:** O(k)=O(log2n) //for answering query

RANGE MINIMUM QUERIES (RMQ):
---
-> processinga value in range once or more does not matter leading to an advantage\
-> instead of splitting range into multiples ranges, just need to split into only 2 overlapping ranges with power of two length.\
-> for finding min of the range [l,r] with:
```cpp
    min (st[l][j], st[r-2^(j)+1][j])  where j = log2(r-l+1)
```
--> precomputing sparse table structure with f(x,y)=min(x,y)
```cpp
int st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = min(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);
```
-->min of range [l,r] can be computed with:
```cpp
int j = log[R - L + 1];
int minimum = min(st[L][j], st[R - (1 << j) + 1][j]);
```
-> ** COMPLEXITY OF RMQ:** O(1)\
-> Complexity of O(1) can be achieved for functions like sum using disjoint sparse table or sqrt tree

TEMPLATE:
---
```cpp
 
#include<bits/stdc++.h>
using namespace std;
#define ll long long int
#define llu long long unsigned int
#define ld long double
typedef pair<ll,ll> l_l;
typedef pair<int,int> i_i;
ll mod=1000000007;
//ll n;
template<typename T>
struct sparse{
	vector<vector<T>> sp;
    vector<int> lg;
    const int k=25;
    int n;
	void init(int N){
		sp.assign(N,vector<T>(k+1));
        n=N;
        lg.assign(N+1,0);
        lg[1]=0;
		for(int i=2;i<=N;i++){
			lg[i]=lg[i/2]+1;
		}
	}
	void build(T a[]){
		for(int i=0;i<n;i++){
			sp[i][0]=a[i];
		}
		for(int j=1;j<=k;j++){
			for(int i=0;i+(1<<j)<=n;i++){
				sp[i][j]=__gcd(sp[i][j-1],sp[i+(1<<(j-1))][j-1]);
			}
		}
	}
	T query(T l,T r){
		int fin=lg[r-l+1];
		return __gcd(sp[l][fin],sp[r-(1<<fin)+1][fin]);
	}
	T sum(T l,T r){
		ll sum=0;
		for(int j=k;j>=0;j--){
			if((1<<j)<=(r-l+1)){
				sum+=sp[l][j];
				l+=(1<<j);
			}
		}
		return sum;
	}
};
```

PROBLEMS:
---
1. [Codechef practice -- MATCHSTICKS](https://www.codechef.com/problems/MSTICK)

