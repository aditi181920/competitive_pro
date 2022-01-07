**COUNTING INVERSIONS IN AN ARRAY**
--

1. **BRUTE FORCE:**
---

```cpp
int inversion_cnt(int arr[],int n){
    int cnt=0;
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(arr[i]>arr[j]){
                cnt+=1;
            }
        }
    }
}
COMPLEXITY: O(n^2)
```

2. **MERGE SORT:**
---

Idea: When merging 2 sorted array if left[i] > right [j] then this right[j] is smaller than all the next upcoming elements in left so, inv cnt can be increased by (size of left array)-i\
Rest all can be implemented like std merge sort algorithm\

```cpp
class Solution{
  public:
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    long long int merge(long long int arr[], long long int l,long long int q, long long int r){
    long long int cnt=0;
    long long int n1=q-l+1,n2=r-(q+1)+1;
    long long int left[n1],right[n2];
    int id=l;
    for(int i=0;i<n1;i++){
        left[i]=arr[id];
        id++;
    }
    for(int i=0;i<n2;i++){
        right[i]=arr[id];
        id++;
    }
    long long int i=0,j=0,k=l;
    while(i<n1 && j<n2){
        if(left[i]>right[j]){
            cnt+=((n1-1)-i+1);
            arr[k]=right[j];
            j++;
            k++;
        }else{
            arr[k]=left[i];
            i++;
            k++;
        }
    }
    while(i<n1){
        arr[k]=left[i];
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
long long int mergesort(long long int arr[],long long int l,long long int r){
    long long int cnt=0;
    if(l<r){
        int q=(l+r)/2;
        cnt+=mergesort(arr,l,q);
        cnt+=mergesort(arr,q+1,r);
        cnt+=merge(arr,l,q,r);
      //  cout<<"l:"<<l<<"  r:"<<r<<"  cnt:"<<cnt<<"\n";
        return cnt;
    }else return 0;
}
long long int inversionCount(long long int arr[], long long int N)
{
    // Your Code Here
    return mergesort(arr,0,N-1);
    
}

};
COMPLEXITY: O(nlogn)
log n levels in divide and conquer and full traversal of n in each level
```



3. **BINARY INDEXED TREE/FENWICK TREE:**
---

We can start inserting elements in BIT and if we are inserting elements from :\
-> right : add number of elements less than this value added previously (that is occuring to right of it) to inv cnt
-> left : add number of elements greater than this value added previously(that is occuring to left of it)(no. of elements added- elements less than or eq to it added) to inv cnt

```cpp
class Solution{
  public:
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    struct fen{
        vector<long long int> bit;
      fen(int n){
          bit.resize(n+1,0);
      }
      void update(int x,int val){
          for(int i=x;i<bit.size();i+=(i&(-i))){
              bit[i]+=val;
          }
      }
      long long int query(int x){
          long long int res=0;
          for(int i=x;i>0;i-=(i&(-i))){
              res+=bit[i];
          }
          return res;
      }
    };
    long long int inversionCount(long long arr[], long long n)
    {
        // Your Code Here
        long long int mx=0;
        for(int i=0;i<n;i++){
            mx=max(mx,arr[i]);
        }
        fen f(mx);
        long long int ans=0;
        for(int i=n-1;i>=0;i-- ){
            ans+=f.query(arr[i]-1);
            f.update(arr[i],1);
        }
        return ans;
    }

};
COMPLEXITY:
O(log maxelement) for query and update function
also we have to query for each element so total complexity comes out to be:
O(n log maxelement)
Note: this code won't work if negative numbers appears as bit index cannot be negative in that case we have 
to fist normalize whole array values to a positive range
```

4. **STL SET:**
---
the idea is quite the same that was used for fenwick tree before 
we are just using set's property of ordering itself in logn time and lower_bound() 
-> insert a[i] into set
-> find the first element greater than a[i] in set using upper_bound() 
-> find dist of above found element from the last element in set and add this distance to inversion cnt
```cpp
#include<bits/stdc++.h>
using namespace std;
int getInvCount(int arr[],int n)
{
    multiset<int> set1;
    set1.insert(arr[0]);
    int invcount = 0; 
    multiset<int>::iterator itset1;
    for (int i=1; i<n; i++)
    {
        set1.insert(arr[i]);
  
        // Set the iterator to first greater element than arr[i]
        // in set (Note that set stores arr[0],.., arr[i-1]
        itset1 = set1.upper_bound(arr[i]);
  
        // Get distance of first greater element from end
        // and this distance is count of greater elements
        // on left side of arr[i]
        invcount += distance(itset1, set1.end());
    }
  
    return invcount;
}
  
int main()
{
    int arr[] = {8, 4, 2, 1};
    int n = sizeof(arr)/sizeof(int);
    cout << getInvCount(arr,n);
    return 0;
}
```

**OPTIMIZED INVERSION COUNT ALGO:**
---
-> the fenwick tree approach can be optimized further by combining it with the idea of sqrt decomposition.
```cpp
#pragma GCC optimize ("Ofast")
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
#define llu long long unsigned int
#define ld long double
//const ll mod=1000000007;
const ll mod=998244353;
const int M=6e4;
const int SQR=1005;
const int N=3e5;
//struct fen{
	//vector<ll> bit;
	ll bit[SQR][M]={0};
	ll st[SQR],fin[SQR];
	ll b[N];
	//fen(int n){
	//	bit.resize(n+1);
	//	bit.resize(SQR,vector<ll> (M));
//		b.resize(n+5);
//		st.resize(SQR);
//		fin.resize(SQR);
//	}
	void update(int b,int x,ll v){
		for(int i=x;i<M;i+=(i&(-i))){
			bit[b][i]+=v;
		}
	}
	ll query(int b,int x){
		ll ans=0;
		for(int i=x;i>0;i-=(i&(-i))){
			ans+=bit[b][i];
		}
		return ans;
	}
	ll range_query(ll l,ll r,ll x,vector<ll> &a){
		int stblock=b[l],endblock=b[r];
		ll ans=0;
		for(int i=stblock;i<=endblock;i++){
			if(st[i]>=l && fin[i]<=r){
				ans+=query(i,x);
			}else{
				for(int j=max(st[i],l);j<=min(r,fin[i]);j++){
					ans+=(a[j]<=x);
				}
			}
		}
		return ans;
	}
//};
int main(){
  //  int t;
    fast_io;
  //  cin>>t;
  //  while(t--){
        int n;
        cin>>n;
	//	fen bit(n+1);
        vector<ll> a(n+1);
		for(int i=1;i<=n;i++)cin>>a[i];
		int bno=1;
		for(int i=1;i<=n;){
			int j=i;
			st[bno]=j;
			while(j<=n && j<i+SQR){
				//cin>>a[j];
				update(bno,a[j],1);
				b[j]=bno;
				j++;
			}
			fin[bno]=j-1;
			bno++;
			i=j;
		}
		ll cnt=0;
		for(int i=n;i>=1;i--){
			cnt+=query(0,a[i]-1);
			update(0,a[i],1);
		}
		int q;
		cin>>q;
		while(q--){
			ll x,y;
			cin>>x>>y;
			//first find no. of numbers greater than a[x] in 1 to x-1 
			//eq to elements- no. of elements less than eq to a[x] in 1 to x-1
			//then find no. of numbers leass than eq to a[x]-1 in x+1 to n
			//remove these inversions from cnt
			// again find same things after a[x]=y and add them in inversion cnt
			ll g1=range_query(1,x-1,a[x],a);
			g1=x-1-g1;
			ll g2=range_query(x+1,n,a[x]-1,a);
			cnt-=(g1+g2);
			update(b[x],y,1);
			update(b[x],a[x],-1);
			a[x]=y;
			g1=range_query(1,x-1,a[x],a);
			g2=range_query(x+1,n,a[x]-1,a);
			cnt+=(x-1-g1);
			cnt+=g2;
			cout<<cnt<<"\n";
		}
 
   // }
    return 0;
}
```
