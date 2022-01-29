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
