**Z function:**
--

z[i] = length of longest string that is at the same time, a prefix of s and a prefix of the suffix of s starting at i\
z[0] is generally not well defined- we can assume it zero
(isn't this same def in KMP? ok KMP is a bit different it is longest suffix ending at i which is prefix and z function is longest suffix starting at i which is prefix)
Example:\
"aaabaab": [0,2,1,0,2,1,0]

-> so how this algo works is we define z blocks ... now let's say we got a matching with first character if it matches then match next with second.. so goes on until u can keep on matching and that forms a z block\
-> so now the since this block matches with the prefix.. and we have already computed the values for the prefix so we can copy every next character in this block with the precomputed values\
-> there is one catch though\
-> if the value exceeds the block size or just touches it .. we don't know about things outside block so for that we can limit the value till the boundary and we can continue checking further on their turns 

```cpp
#include "bits/stdc++.h"
using namespace std;
#define ll long long int
#define mp make_pair
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
//-----constants---------------
ll llmx=1e15;
ll llmn=-1e15;
const ll mod =998244353;
//const ll mod=1000000007;
#define ll long long int
ll bexp(ll a,ll b){
    ll res=1;
    a%=mod;
    while(b>0){
        if(b&1){
            res=res*a%mod;
        }
        a=a*a%mod;
        b>>=1;
    }
    return res;
}
int main(){
  fast_io;
  int n;
  cin>>n;
  int q;
  cin>>q;
  int ans=q;
  vector<vector<int>> seg(n+1);
  while(q--){
    int l,r;
    cin>>l>>r;
    seg[l].push_back(r);
  }
  //we can create 2^q seg 
  //now we need to remove overcounting
  //segments that can be obtained by intersection of 2 segments we need to remove their contribution
  //how to find these segments
  //we go through increasing order of lower bound 
  //now for every element of same lower bound 
  //we push the seg created by their intersection .. to check if they  are invalid or they end up creating some invalid seg 
  //why does this always work 
  //that is cover all overcounting cases and no extra reduction leading to undercounting?
  //becuase if some intersection leads to creation of some seg/segments that exist=> all seg involved exist=> in whatever order u take it u will alwayas get 1 seg existing 
  //there for for our convience we go from left to right thereby checking every seg that can be created by taking 2 lefts common 
  //but wait there can be a case that 3rd and 4th left creates an ocuring 
  //or 3rd and 5th 
  //how to reduce n*n case
  //okay so how this works is 
  //notice that there are a lot of segments take all together lead to 1 seg 
  //now we can always remove leftmost common subseg first
  //then the segment that remains either it is the last segment that overlaps or we need to remove some segments from ths 
  //so again what we remove is the leftmost common subsegment 
  //in the end we are left with 2 segments 1 left by removing all other mixed segments and 1 the segment that coincides with this one 
  //what if we achieve a segment which is present and there is more segments present inside 
  //no problem this is cool we can just keep on divind this 

  for(int i=0;i<n+1;i++){
    sort(seg[i].begin(),seg[i].end());
    for(int j=1;j<seg[i].size();j++){// cout<<"i:"<<i<<" j:"<<j<<"\n";
      int nwl=seg[i][0]+1;  
      int nwr=seg[i][j];    //cout<<seg[i][0]<<" "<<seg[i][j]<<" "<<nwl<<" "<<nwr<<"\n";
      if(nwl>nwr){ //cout<<"ok\n";
        ans-=1;
      }else seg[nwl].push_back(nwr);
    }
  }
  //cout<<ans<<"\n";
  cout<<bexp(2,ans)<<"\n";
  return 0;
}
```
