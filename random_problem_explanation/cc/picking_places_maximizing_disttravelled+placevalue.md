PROBLEM STATEMENT:
--

Input:\
-> Number of places(n)\
-> Number of places we want to visit (k)[k is always even]\
-> Position (x<sub>i</sub>) and exploring time (s<sub>i</sub> hours) for each place. \
Given : Time needed to move 1 unit distance is 1 hour. \
Objective: We want to visit k distinct places with highest boredomness. Boredomness of a trip is total time wasted (time spent while moving between places+time spent exploring the places). Formally if visiting an array p=[p1,p2,p3,...,pk] then boredomness equals 
 

![ \sum_{i=2}^{k}|x_{p_{i}}-x_{p_{i-1}}|+\sum_{i=1}^{k}s_{p_i}](https://latex.codecogs.com/svg.image?%20%5Csum_%7Bi=2%7D%5E%7Bk%7D%7Cx_%7Bp_%7Bi%7D%7D-x_%7Bp_%7Bi-1%7D%7D%7C&plus;%5Csum_%7Bi=1%7D%5E%7Bk%7Ds_%7Bp_i%7D)


Constraints:\
-> 2<=k<=n<=2.10<sup>7</sup>\
-> k is even\
-> -10<sup>9</sup><=x<sub>i</sub><=10<sup>9</sup>\
-> 1<=s<sub>i</sub><=10<sup>9</sup>



Test case 1:

INPUT:\
7\
4\
0 3\
1 7\
2 4\
3 9\
4 5\
5 7\
6 4

OUTPUT:\
39

EXPLANATION:\
 The trip with the maximum boredomness is [4,7,2,6]\
The boredomness can be calculated using the given formula.

SOLUTION:
--

HINT 1:\
-> Use the constraint k/2 somehow

HINT 2:\
-> Can you find out the effective contribution for k/2 places from left half and similarly from right half

HINT 3:\
-> How can you merge these two halves?

SOLUTION EXPLANATION:
---

-> if i go to places in order (sorted) then all xi's except start and end will be deleted we will be left with -xi of first place and +xi of last place that's it since we are entering and leaving to go ahead\
-> but notice if we don't follow the order we actually get -2\*xi for each xi in left except last xi which will be -xi only and similarly +2\*xi for each xi in the right except first xi of right which will be +xi\
-> we can easily see that the second way will give greater distances [as we have k/2 +ve in right and k/2 -ve in left so we can form k/2 positive term of (xi-xj) form combining left and right so we have additional positive terms than positive]\

-> now we know left's position contributes negatively so we have to take highest value of left as -xi (because if it is -2xi it will contribute more negatively)\
-> similarly right's position contributes positively so we have to take lowest value of right as +xi ( because higher xi's +2xi will contribute more positively so we should not use any higher value )

-> now for left k/2 positions we can start iterating from start and keep pushing values in priority queue if at some point size of queue becomes k/2-1 then we have to take next pos's contribution +xi if we consider next xi as the last left place \
-> we need to update a[i] as the contribution of left k/2 places such that ith place is the k/2th place in left\
-> we can pop min contributing place from priority queue whenever it exceeds size before moving to next place and update a[i] for each i

-> similarly for right k/2 positions , here we start iterating from the end and keep operating similarly just adjust the contribution values (+ instead of -)\
-> b[i] now indicates contribution of right k/2 places such that ith place is the first place in right

-> now we have a[i] and b[i] calculated \
-> we need to merge them\
-> we know a[i] can only be merged with b[j] where j>i according to definition of a[i] and b[i] \
-> now we know while traversing a[i] from start we can take any b[j] with j>i \
-> how can i find optimal merger in O(n) time?\
-> well if i transition from a[i] to a[i+1] i can't consider b[i+1] anymore \
-> so if b[i+1] contributes somehow to optimal merger we have to consider it before reaching a[i+1]\
-> also if we keep updating a[i+1] with max(a[i+1],a[i] ) we will always have max left k/2 value \
-> now at some point let;s say i we just have to consider if a[i]+b[i+1] improves our answer \
-> because if this a[i] gives optimal merger then if b[i+1] is optimal merger of right then good else we will definitely get the optimal one later as a[i] will always be updated to each a[i1] as it is optimal left merger \
-> if a[i] is not then sme a[j] with j>i must be optimal left merger and for that optimal right will always lie ahead only again due to definition of a[i] and b[i] now it reduces to above case

-> so merger should be just\
-> update ans if a[i]+b[i+1] is greater\
-> update a[i+1] to max(a[i],a[i+1])

**IMPLEMENTATION:**
---

```cpp
#pragma GCC optimize ("Ofast")
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
using namespace std;
#define ll long long int
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
#define llu long long unsigned int
#define ld long double
#define f first 
#define s second
#define mp make_pair
const ll big=2000000000;
//const ll mod=1000000007;
int main(){
    fast_io; 
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        int k;
        cin>>k;
        vector<vector<ll>> arr(n,vector<ll> (2));
        for(int i=0;i<n;i++){
            cin>>arr[i][0]>>arr[i][1];
        }
        sort(arr.begin(),arr.end());
        priority_queue<ll,vector<ll>,greater<ll>> q;
        ll sum=0;
        vector<ll> a(n,-1e18),b(n,-1e18);
        k/=2;
        k--;
        for(int i=0;i<n;i++){
            if(q.size()==k){
                a[i]=sum-arr[i][0]+arr[i][1];
            }
            ll tmp=arr[i][1]-2*arr[i][0];
            q.push(tmp);
            sum+=tmp;
            if(q.size()>k){
                sum-=q.top();
                q.pop();
            }
        }
        sum=0;
        while(!q.empty())q.pop();
        for(int i=n-1;i>=0;i--){
            if(q.size()==k){
                b[i]=sum+arr[i][1]+arr[i][0];
            }
            ll tmp=arr[i][1]+2*arr[i][0];
            sum+=tmp;
            q.push(tmp);
            if(q.size()>k){
                sum-=q.top();
                q.pop();
            }
        }
        ll ans=-1e18;
        for(int i=0;i<n-1;i++){
            ans=max(ans,a[i]+b[i+1]);
            a[i+1]=max(a[i+1],a[i]);
        }
        cout<<ans<<"\n";
    }
    return 0;
}
```

**PROBLEM LINK:**
---
[COOKOFF DIV2 BT](https://www.codechef.com/COOK137B/problems/BT)
