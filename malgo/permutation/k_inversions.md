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
**USING MERGESORT:**
```cpp
the idea is somewhat the same
for every merge we store in buffer the inversions that right element being merged will create with respect to 
every left element being merged and add this buffer count to left elements being merged as that will be the
total inversions that left element will be responsible for all the right elements being merged
since in merge sort the way merges are done every smaller element will be compared with every element
greater than it appearing left to it so this will work fine 
also we have to store index because the item are getting rearranged so we must know its original index to update
the the inversions with respect to element at that index 


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
long long int merge(vector<pair<ll,int>> &arr, long long int l,long long int q, long long int r,ll b[],ll nb[]){
    long long int cnt=0;
    long long int n1=q-l+1,n2=r-(q+1)+1;
    vector<pair<ll,int>> left(n1),right(n2);
    int id=l;
    for(int i=0;i<n1;i++){
        left[i]=arr[id];
        id++;
    }
    for(int i=0;i<n2;i++){
        right[i]=arr[id];
        id++;
    }
    long long int i=0,j=0,k=l,add=0;
    while(i<n1 && j<n2){
        if(left[i].first>right[j].first){
	//		cout<<"l:"<<l<<"  q:"<<q<<"  r:"<<r<<"  i:"<<i<<"  j:"<<j<<"  b[j]:"<<b[j]<<"\n";
	//		cout<<"leftid:"<<left[i].second<<" arr[q+1].idx:"<<arr[q+1].second<<"  rightid:"<<right[j].second<<"\n";
    //        cnt+=((n1-1)-i+1);
			add+=b[right[j].second];
			add%=mod;
			//nb[left[i].second]+=add; overcounting as this left will be probably inserted in else part or in next while
            arr[k]=right[j];
            j++;
            k++;
        }else{
            arr[k]=left[i];
			nb[left[i].second]+=add;
			nb[left[i].second]%=mod;
            i++;
            k++;
        }
    }
    while(i<n1){
        arr[k]=left[i];
		nb[left[i].second]+=add;
		nb[left[i].second]%-mod;
        k++;
        i++;
    }
    while(j<n2){
        arr[k]=right[j];
        j++;
        k++;
    }
    return cnt;
}
long long int mergesort(vector<pair<ll,int>> &arr,long long int l,long long int r,ll b[],ll nb[]){
    long long int cnt=0;
    if(l<r){
        int q=(l+r)/2;
        cnt+=mergesort(arr,l,q,b,nb);
        cnt+=mergesort(arr,q+1,r,b,nb);
        cnt+=merge(arr,l,q,r,b,nb);
      //  cout<<"l:"<<l<<"  r:"<<r<<"  cnt:"<<cnt<<"\n";
        return cnt;
    }else return 0;
}
long long int inversionCount(vector<pair<ll,int>> &arr, long long int N,ll b[],ll nb[])
{
    // Your Code Here
    return mergesort(arr,0,N-1,b,nb);
    
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
		vector<pair<ll,int>> a(n);
		for(int i=0;i<n;i++){
			cin>>a[i].first;
			a[i].second=i;
		}
		ll b[n];
		for(int i=0;i<n;i++)b[i]=1;
	//	for(int i=0;i<n;i++)cout<<b[i]<<" ";
		//cout<<"\n";
		ll ans=0;
		ll nb[n+1]; nb[n]=0;
		vector<pair<ll,int>> aux(n);
		//for(int i=0;i<=n;i++)nb[i]=0;
		for(int i=2;i<=k;i++){
			for(int i=0;i<n;i++){
				nb[i]=0;
			}
			for(int i=0;i<n;i++){
				aux[i]=a[i];
			}
			inversionCount(aux,n,b,nb);
		//	cout<<"nb:";
	//		for(int i=0;i<n;i++){
	//			cout<<nb[i]<<" ";
	//		} cout<<"\n";
		//	for(int i=1;i<=n;i++){
	//			nb[i]+=nb[i-1];
//			}
	      //  memset(b,0,sizeof(b));
	        for(int i=0;i<n;i++){
				b[i]=abs(nb[i]);
			}
	//		for(int i=0;i<n;i++){
	//			cout<<b[i]<<" ";
	//		} cout<<"\n";
		}
		for(int i=0;i<n-(k-1);i++){
			ans+=abs(b[i]);
			ans%=mod;
		}
		cout<<ans<<"\n";
   //}
    return 0;
}
```
