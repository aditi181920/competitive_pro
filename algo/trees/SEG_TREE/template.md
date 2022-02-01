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
