**STANDARD SEG TREE:**
---

```cpp
template<typename Tnode,typename Tup>
struct segt{
    vector<Tnode> seg;
    int sz;
    segt(int n){
        sz=n;
        seg.resize(4*n);
    }
    Tnode merg(Tnode a,Tnode b){
        Tnode c;
        c= min(a,b); 
        return c;
    }
    void build(vector<Tnode> &a){
        build(1,0,sz-1,a);
    }
    void build(int node,int l,int r,vector<Tnode> &a){
        if(l==r){
            seg[node]=a[l];
            return;
        }
        int mid=(l+r)>>1;
        build(2*node,l,mid,a);
        build(2*node+1,mid+1,r,a);
        seg[node]=merg(seg[2*node],seg[2*node+1]);
    }
    void update(int id,Tup v){
        update(1,0,sz-1,id,v);
    }
    void update(int node,int l, int r, int id,Tup v){
        if(l==r){
            seg[node]=v;
            return;
        }
        int mid=(l+r)>>1;
        if(id<=mid){
            update(2*node,l,mid,id,v);
        }else update(2*node+1,mid+1,r,id,v);
        seg[node]=merg(seg[2*node],seg[2*node+1]);

    }
    Tnode query(int l,int r){
        return query(1,0,sz-1,l,r);
    }
    Tnode query(int node,int l,int r,int x,int y){
        if(l>=x && r<=y)return seg[node];
        int mid=(l+r)>>1;
        if(y<=mid) return query((2*node),l,mid,x,y);  //range lies in left segment
        if(x>mid) return query(2*node+1,mid+1,r,x,y);   //range lies in right segment
        return merg(query((2*node),l,mid,x,y),query(2*node+1,mid+1,r,x,y));  //range lies in between
    }
};
```

**PROBLEM LINKS:**\
[CF 768 DIV2 E](https://codeforces.com/contest/1631/problem/E)

**SEG TREE WITH LAZY PROPAGATION:**
--

```cpp

int mx=1e8;
int mn=-1e8;
struct item{
    int res,lzy_add,lzy_ass,id;
};
struct segt{
    vector<item> seg;
    item init={mx,0,mn,-1};
    int sz;
    segt(int n){
        sz=n;
        seg.resize(4*n);
    }
    item merg(item a,item b){
        int c;
      //  (a.res<b.res)?c=a.id:c=b.id;
        if(a.res<=b.res)c=a.id;
        else c=b.id;
        return {min(a.res,b.res),0,mn,c};
    }
    void build(vector<int> &a){
        build(1,0,sz-1,a);
    }
    void build(int node,int tl,int tr,vector<int> &a){
        if(tl==tr){
            seg[node]=init;
            seg[node].res=a[tl];
            seg[node].id=tl;
            return;
        }
        int mid=(tl+tr)>>1;
        seg[node]=init;
        build(2*node,tl,mid,a);
        build(2*node+1,mid+1,tr,a);
        seg[node]=merg(seg[2*node],seg[2*node+1]);
    }
    void prop(int &node,int &tl,int &tr){
        //first is new num has been assigned then prop that
        if(seg[node].lzy_ass!=mn){
            seg[node].res=seg[node].lzy_ass;
            seg[node].id=tl;
            if(tl<tr){
                seg[2*node]=seg[2*node+1]=init;
                seg[2*node].lzy_ass=seg[node].lzy_ass;
                seg[2*node+1].lzy_ass=seg[node].lzy_ass;
            }
            seg[node].lzy_ass=mn;
        }
        seg[node].res+=seg[node].lzy_add;
        if(tl<tr){
            seg[2*node].lzy_add+=seg[node].lzy_add;
            seg[2*node+1].lzy_add+=seg[node].lzy_add;
        }
        seg[node].lzy_add=0;
    }
    void update(int &l,int &r,int &v){
        update(1,0,sz-1,l,r,v);
    }
    void update(int node,int tl, int  tr, int &l,int &r,int &v){
        prop(node,tl,tr);
        if(tl>r or tr<l)return;
        if(tl>=l & tr<=r){
            seg[node]=init;
            seg[node].lzy_ass=v;
            prop(node,tl,tr);
            return;
        }
        int mid=(tl+tr)>>1;
        update(2*node,tl,mid,l,r,v);
        update(2*node+1,mid+1,tr,l,r,v);
        seg[node]=merg(seg[2*node],seg[2*node+1]);

    }
    void add(int &l,int &r,int &v){
        add(1,0,sz-1,l,r,v);
    }
    void add(int node,int tl, int tr, int &l,int &r,int &v){
        prop(node,tl,tr);
        if(tl>r or tr<l)return;
        if(tl>=l && tr<=r){
            seg[node].lzy_add+=v;
            prop(node,tl,tr);
            return;
        }
        int mid=(tl+tr)>>1;
        add(2*node,tl,mid,l,r,v);
        add(2*node+1,mid+1,tr,l,r,v);
        seg[node]=merg(seg[2*node],seg[2*node+1]);

    }
    item query(int &l,int &r){
        return query(1,0,sz-1,l,r);
    }
    item query(int node,int tl,int tr,int &l,int &r){
      //  if(tl>r or tr<l)return init;
        prop(node,tl,tr);
        if(tl>r or tr<l)return init;
        if(tl>=l && tr<=r)return seg[node];
        int mid=(tl+tr)>>1;
        item i1= query((2*node),tl,mid,l,r);  //range lies in left segment
        item i2= query(2*node+1,mid+1,tr,l,r);   //range lies in right segment
        return merg(i1,i2);  //range lies in between
    }
};
```

**PROBLEM LINKS:**\

[CC JAN LT 2022 DIV2](https://www.codechef.com/LTIME104B/problems/CIRCPRMRCVRY)


**SEG TREE FINDING FIRST ELEMENT ON LEFT AND RIGHT WITH SOME CONDITION:**
--

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define ld long double 
#define mp make_pair
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
//-----constants---------------
ll llmx=1e15;
ll llmn=-1e15;
const ll mod =998244353;
//const ll mod=1000000007;
//const int N = 5e5 + 5;
const int SN = 1 << 20;
const long long inf = 1e16 + 16;
//-----containers--------------
 
template<typename T>
struct segt{
    struct node{         //->seg node
        T mx=0,mn=0,lzy=0;
        void apply(T v){
            mn+=v;
            mx+=v;
            lzy+=v;
        }
    };
    node merge(const node&x, const node&y){   //->merging nodes
        node ans;
        ans.mn=min(x.mn,y.mn);
        ans.mx=max(x.mx,y.mx);
        return ans;
    }
    vector<node> seg;
    int n;
    void init(int n){                 //->initialize and build
        this->n=n;
        seg.resize(2*n-1);  
        build(0,0,n-1);  
    }
    void init(int n,vector<T> &a){
        this->n=n;
        seg.resize(2*n-1);
        build(0,0,n-1,a);
    }
    void push(int x,int l,int r){           //pushing the information down the tree
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        if(seg[x].lzy!=0){
            seg[x+1].apply(seg[x].lzy);
            seg[z].apply(seg[x].lzy);
            seg[x].lzy=0;
        }
    }
    void pull(int x,int z){                     //merging the child values at parent
        seg[x]=merge(seg[x+1],seg[z]);
    }
    void build(int x,int l,int r){// cout<<"x:"<<x<<"  l:"<<l<<" r:"<<r<<"\n";
        if(l==r){
            return; //we are building empty segtree 
        }
        int y=(l+r)>>1;
        int z=(x+((y-l+1)<<1));
        build(x+1,l,y);
        build(z,y+1,r);
        pull(x,z);
    }
    void build(int x,int l,int r,vector<T> &a){
        if(l==r){
            seg[x].apply(a[l]);
            return;
        }
        int y=(l+r)>>1;
        int z=(x+((y-l+1)<<1));
        build(x+1,l,y,a);
        build(z,y+1,r,a);
        pull(x,z);
    }
    node get(int x,int l,int r,int ql,int qr){   //query function for seg tree
        if(ql<=l && r<=qr){
            return seg[x];
        }
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        push(x,l,r);
        node res;
        if(qr<=y){
            res=get(x+1,l,y,ql,qr);
        }else if(ql>y){
            res=get(z,y+1,r,ql,qr);
        }else{
            res=merge(get(x+1,l,y,ql,min(qr,y)),get(z,y+1,r,max(ql,y+1),qr));
        }
        pull(x,z);
        return res;
    }
    node get(int l,int r){
        return get(0,0,n-1,l,r);
    }
    node get(int p){
        return get(0,0,n-1,p,p);
    }
     void modify(int x,int l,int r,int ql,int qr,T v){       //modify function for segtree
        if(ql<=l && r<=qr){
            seg[x].apply(v);
            return;
        }
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        push(x,l,r);
        node res;
        if(ql<=y){
            modify(x+1,l,y,ql,min(y,qr),v);
        }
        if(qr>y){
            modify(z,y+1,r,max(y+1,ql),qr,v);
        }
        pull(x,z);
    }
    void modify(int l,int r,T v){
        modify(0,0,n-1,l,r,v);
    }
    int go1(int x,int l,int r,const function<bool(const node&)> &f){   //finding first element that satisfies condition
        if(l==r)return l;
        push(x,l,r);
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        int res;
        if (f(seg[x+1])) {
        res =go1(x+1,l,y,f);
        } else {
        res =go1(z,y+1,r,f);
        }
        pull(x,z);
        return res;
    }
    int find_first(int x,int l,int r,int ql,int qr,const function<bool(const node&)>&f){  //find leftmost candidate seg that may have it
        if(ql<=l && r<=qr){
            if(!f(seg[x]))return -1;
            return go1(x,l,r,f);
        }
        push(x,l,r);
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        int res=-1;
        if(ql<=y){
            res=find_first(x+1,l,y,ql,qr,f);
        }
        if(qr>y && res==-1){
            res=find_first(z,y+1,r,ql,qr,f);
        }
        pull(x,z);
        return res;
    }
    int ff(int l,int r,const function<bool(const node&)> &f){
        return find_first(0,0,n-1,l,r,f);
    }
    int go2(int x,int l,int r,const function<bool(const node&)> &f){
        if(l==r)return l;
        push(x,l,r);
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        int res;
        if (f(seg[z])) {
        res =go2(z,y+1,r,f);
        } else {
        res =go2(x+1,l,y,f);
        }
        pull(x,z);
        return res;
    }
    int find_last(int x,int l,int r,int ql,int qr,const function<bool(const node&)>&f){
        if(ql<=l && r<=qr){
            if(!f(seg[x]))return -1;
            return go2(x,l,r,f);
        }
        push(x,l,r);
        int y=(l+r)>>1;
        int z=x+((y-l+1)<<1);
        int res=-1;
        if(qr>y){
            res=find_first(z,y+1,r,ql,qr,f);
        }
        if(ql<=y && res==-1){
            res=find_first(x+1,l,y,ql,qr,f);
        }
        pull(x,z);
        return res;
    }
    int fl(int l,int r,const function<bool(const node&)> &f){
        return find_last(0,0,n-1,l,r,f);
    }
};
```

**PROBLEM LINK**
--

[CF 807 DIV2](https://codeforces.com/contest/1705/problem/E)
