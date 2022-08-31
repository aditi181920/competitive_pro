**Template of fenwick tree operations:**
--


```cpp

struct fen{
    vector<ll> ar;
    //in fenwick tree each number stores their own region of responsibililty
    //so we store the numbers at their own position and add to all the region of responsibility that cover that position
    //we can iteratre through all such regions by adding 1 to the last set bit
    //consider 1 based indexing
    int n;
    fen(int n){
        ar.resize(n+2,llmn);
        n=n+2;
    }
    fen(vector<ll> a):fen(a.size()){
        for(int i=1;i<a.size();i++){
            add(i,a[i]);
        }
    }
    void add(int i,ll v){
        //since we will follow 1 index based bit 
        //indexing starts from 1 therefor ++i
        for(++i ; i<n;i+=(i&(-i))){
            ar[i]=max(ar[i],v);
        }
    }
    void upd(ll &id,ll &val,vector<ll> &a){
     ll extra=val-a[id];
     if(extra<0)extra+=mod;
     add(id,extra);
     a[id]=val;
   }
   void create(vector<ll> &a){
     for(ll i=1;i<=n;i++){
       add(i,a[i]);
     }
   }
    ll query(int id){
        //querying this we need to cover all independent range of reposibilities that comes in the path
        ll ans=llmn;
        for(++id;id>=1;id-=(id&(-id))){
            ans=max(ans,ar[id]);
        }
        return ans;
    }
    
    
   

};

```

```cpp
 //2d fenwick tree
    ll bits[1005][1005];
void add(int ht,int wt){
    //to add something with height and weight
    for(int i=ht;i<1005;i+=((i&(-i)))){
        for(int j=wt;j<1005;j+=(j&(-j))){
            bits[i][j]+=(ht*wt);
        }
    }
}
ll query(int ht,int wt){
    ll ans=0;
    for(int i=ht;i>0;i-=((i&(-i)))){
        for(int j=wt;j>0;j-=(j&(-j))){
            ans+=bits[i][j];
        }
    }
    return ans;
}
ll queryrange(int x,int y,int x1,int y1){
    if(abs(x1-x)<=1 || abs(y1-y)<=1)return 0;
    ll ans=query(x1-1,y1-1);
    ans-=query(x1-1,y);
    ans-=query(x,y1-1);
    ans+=query(x,y);
    return ans;
}
```

**PROBLEM LINKS**
--

[CF 817 DIV4](https://codeforces.com/contest/1722/problem/E)
