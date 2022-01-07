Consider a permutation a1, a2, …, an (all ai are different integers in range from 1 to n). 
Let us call k-inversion a sequence of numbers i1, i2, …, ik such that 1 ≤ i1 < i2 < … < ik ≤ n and ai1 > ai2 > … > aik. 
Your task is to evaluate the number of different k-inversions in a given permutation

**USING DP:**
--

```cpp

Idea: 
we can find 2 inversion using fen tree by inserting values from right & finding no. of numbers less than number inserted
now after we have got values of 2 inversion every index is reponsible to create 
using the same idea we can keep extending it for greater number of inversion
for 3 inversions say
after we have found 2 inversion every index is reponsible for those numbers will become the place values instead of 1 
now again we will initialize fen tree to 0 and start inserting 2 inversion count the corresponding index is reponsible for
then we can check how may 2 inversion can be created by numbers less than currently inserted by querying fen tree
we can create these many 3 inversions using the current inserted index or we can say the current inserted index is
responsible for these many 3 inversions 
like this we can find how many k inversions by repeating this process k times starting from 1 place values initially and 
in last query k inversions caused by all the indexes 

#pragma GCC optimize ("Ofast")
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
#define llu long long unsigned int
#define ld long double
//const ll mod=1000000007;
//const ll mod=998244353;
const int mod=1e9;
vector<ll> bit(20009,0);
	void update(int x,ll v){                     //std fen tree implementation
		for(int i=x;i<20009;i+=(i&(-i))){
			bit[i]+=(v%mod);
                        bit[i]%=mod;
		}
	}
	ll query(int x){
		ll ans=0;
		for(int i=x;i>0;i-=(i&(-i))){
			ans+=(bit[i]%mod);
                        ans%=mod;
		}
		return ans;
	}
int main(){
  //  int t;
      fast_io;
  //  cin>>t;
  //  while(t--){
        int n;
        cin>>n;
		int k;
		cin>>k;
		vector<int> a(n),b(n,1);
		for(int &x:a)cin>>x;
		for(int j=1;j<=k;j++){
			bit.assign(n+2,0);
			for(int i=n-1;i>=0;i--){
				update(a[i],b[i]);
				b[i]=query(a[i]-1);
			}
		}
		cout<<query(n)<<"\n";
   //}
    return 0;
}
```
