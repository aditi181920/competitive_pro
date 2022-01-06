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






















Inversion counting with swap queries in (in each query swap elements at any two indices x and y):\
-> nlogn precomputation with seg tree with a bbst in every node\
-> logn^2 per query \
We perform a range query on the value at index X and the value at index Y to determine the number of numbers smaller than either number in the segment between them, and then compute the change in inversions. After that, we update the 2 indices in the segment tree. Each of the log N nodes takes log N time to update, which gives an overall complexity of log2 N.
from bensonlzl's blog on cf

