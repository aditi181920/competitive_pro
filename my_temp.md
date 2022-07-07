**CURRENT CP TEMPLATE:**
--

```cpp


#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
#define llu long long unsigned int
#define ld long double
#define mp make_pair
mt19937 rng(chrono::steady_clock::now().time_since_epoch().count());
//-----constants---------------
const ll big=2000000000;
const ll inf=10000000;
ll llmx=1e15;
ll llmn=-1e15;
int mn=-1e8;
int mx=1e8;
const ll mod =998244353;
//const ll mod=1000000007;
ll limit=20000001;
//const ll N=200005;
const ld pi=3.1415926535;

//------using pragmas------------
#pragma GCC target ("avx2")
#pragma GCC optimization ("O3")
#pragma GCC optimization ("unroll-loops")

//-----------------using pbds--------
#include <ext/pb_ds/assoc_container.hpp> // Common file
#include <ext/pb_ds/tree_policy.hpp>
#include <functional> // for less
using namespace __gnu_pbds;
 
typedef multi_ordered_set tree<int, null_type, less_equal<int>, rb_tree_tag, tree_order_statistics_node_update> multi_set;
typedef ordered_set tree<int, null_type, less<int>, rb_tree_tag,tree_order_statistics_node_update> ordered_set;
 
 
constexpr int md = 998244353;
using mint = Modular<std::integral_constant<decay<decltype(md)>::type, md>>;
 
//----------binary exponentiation------
ll binexp(ll a,ll b){
    ll res=1;
    while(b>0){
        if(b&1){
            res*=a;
            res%=mod;
        }
        a*=a;
        a%=mod;
        b>>=1;
    }
    return res;
}

//--------set comparator
// bool cmp(int x,int y){
//     if(1) return true;
//     else return false;
// }
// multiset<int,decltype(&cmp)> ms(&cmp);


// auto cmp=[&](const int &x,const int &y){
//     return cnt[x]>cnt[y];
// };
// multiset<int,decltype(&cmp)> ms(cmp);

// struct cmp{
//     bool operator()(const int &x,const int &y) const {return cnt[x]>cnt[y];};
// };
// multiset<int,cmp> ms2;

//---- counting the time taken
// chrono::time_point<chrono::system_clock> start, end;
//     start = chrono::system_clock::now();
//     //code
//     end = chrono::system_clock::now();
//     chrono::duration<double> elapsed_seconds = end - start;
//     cerr<<"Time Taken : "<<elapsed_seconds.count() << "s\n";

//------------dsu-------------

struct dsu{
    vector<int> sz,p;
    dsu(int n){
        sz.resize(n);
        p.resize(n);
    }
    int find_set(int v){
        if(v==p[v])return v;
        else return p[v]=find_set(p[v]);
    }
    void union_set(int a,int b){
        a=find_set(a);
        b=find_set(b);
        //we join small to large so since increases by double 
        //joining a to b 
        if(sz[a]>sz[b])swap(a,b);
        p[a]=p[b];
        sz[b]+=sz[a];
    }
};
//lets create segment trees to store prefix ans suffix sums and create range min queries
struct seg{
    vector<ll> segt;
    seg(int n){
        segt.resize(4*n);
    }
    void build(int node,int l,int r,vector<ll> &a){
      //  cout<<"node:"<<node<<" l:"<<l<<" r:"<<r<<"\n";
        if(l>r)return;
        if(l==r){
            segt[node]=a[l];
            return;
            //we are assigining in leaves
        }
        int mid=(l+r)/2;
        //traverse through left child and right child 
        build(2*node,l,mid,a);
        build(2*node+1,mid+1,r,a);
        segt[node]=max(segt[2*node],segt[2*node+1]);
    }
    void update(int node,int l,int r,int val,int pos){
        if(r==l){
            //reached required leaf
            segt[node]=val;
            return;
        }
        int mid=(l+r)/2;
        //only go to the subtree the is required to be traversed
        if(mid>=pos){
            update(node,l,mid,val,pos);
        }else update(node,mid+1,r,val,pos);
        segt[node]=max(segt[2*node],segt[2*node+1]);
    }
    ll query(int node,int l,int r,int ql,int qr){
        if(ql>qr)return llmn;
        if(l==ql && r==qr)return segt[node];
        int mid=(l+r)/2;
        return max(query(2*node,l,mid,ql,min(qr,mid)),query(2*node+1,mid+1,r,max(ql,mid+1),qr));
    }
};
//build fenwick tree
//we need add method
//then query fenwick tree
//we are building a max fen tree
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

//-----centroid decomposition

set<int> g[100005];
int n;
vector<vector<int>> centroid;
vector<map<int,int>> calcdis;
vector<int> sz,par;
int cnt=0;
int ht,lim;
void dfs(int node,int p){               //->calculating size of the subtrees through dfs traversal
  sz[node]=1;
  cnt+=1;
  for(auto x:g[node]){
    if(x!=p){
      dfs(x,node);
      sz[node]+=sz[x];
    }
  }
}
int find_centroid(int  node,int p){         //-> finding centroid
  for(auto x:g[node]){
    if(x==p)continue;
    if(sz[x]>(cnt/2)){
      return find_centroid(x,node);
    }
  }
  return node;
}
void dfsdistance(int c,int node,int p){
  for(auto x:g[node]){
    if(x==p)continue;
    calcdis[c][x]=calcdis[c][node]+1;
    dfsdistance(c,x,node);
  }
}
void create(int p,int root){                       //centroid decomposition
  cnt=0;
  dfs(root,p);                                     //->subtree sizes
  int node=find_centroid(root,p);                  //find centroid 
  if(p!=-1){
    centroid[p].push_back(node);                   //constructing centroid tree
    centroid[node].push_back(p);
  }                                                //now we need to remove every edge of type node->x and x->node removing node to x is easy for x-> node uhm
  par[node]=p;       
  dfsdistance(node,node,-1);                  
  vector<int> ajd(g[node].begin(),g[node].end());                               
  for(auto x:ajd){ 
    g[node].erase(x);
    g[x].erase(node);
    create(node,x);
  }
}

//---------------lca temp-----------------

vector<int> tin,tout;
vector<vector<int>> lca;
int timer=0;
int timer=0;
void calctime(int node,int p){                       //calculate intime and outtimes
  tin[node]=++timer;
  for(auto x:centroid[node]){
    if(x==p)continue;
    calctime(x,node);
  }
  tout[node]=++timer;
}
int isancestor(int x,int y){                          //ancestor function
  if(tin[x]<=tin[y] && tout[x]>=tout[y])return true;
  else return false;
}
int find_lca(int x,int y){                            //lca function
  if(isancestor(x,y))return x;
  if(isancestor(y,x))return y;
  for(int i=lim;i>=0;i--){
    if(lca[x][i]<=0)continue;
    if(!isancestor(lca[x][i],y)){
      x=lca[x][i];
    }
  }
  return lca[x][0];
}
int ht=0; //=---> calc and equate this to height of the tree
int lim=log2(ht)+1;  
  int main(){
    for(int i=1;i<=n;i++)lca[i].resize(lim+1);          //calculation for binary uplifting to calculate lca
  for(int j=0;j<=lim;j++){
    for(int i=1;i<=n;i++){
      if(j==0){
        lca[i][j]=par[i];
      }else{
        if(lca[i][j-1]>0){
          lca[i][j]=lca[lca[i][j-1]][j-1];
        }
      }
    }
  }
  }



```
