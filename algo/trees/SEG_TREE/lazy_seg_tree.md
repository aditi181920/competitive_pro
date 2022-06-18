RANGE UPDATES (LAZY PROPAGATION)
--
  
-> range modification and range query in O(logn)

1. ADDITION ON SEGMENTS:
---
  
  -> add a no. x to all numbers in the segment a[l...r]\
  -> store at each vertex in the seg tree how many we should add to all no.'s in the corresponding segment\
  -> so we only have to change atmost O(log n) many values not all O(n) values\
  -> answering query: go down tree and add up all the values found along the way which contribute to required segment
  
  ```cpp
    void build(int a[], int v, int tl, int tr) {
        if (tl == tr) {
            t[v] = a[tl];
        } 
        else {
            int tm = (tl + tr) / 2;
            build(a, v*2, tl, tm);
            build(a, v*2+1, tm+1, tr);
            t[v] = 0;
        }
    }

    void update(int v, int tl, int tr, int l, int r, int add) {
        if (l > r)
            return;
        if (l == tl && r == tr) {
            t[v] += add;      //updating corresponding segment instead of all values
        } else {
            int tm = (tl + tr) / 2;
            update(v*2, tl, tm, l, min(r, tm), add);
            update(v*2+1, tm+1, tr, max(l, tm+1), r, add);
        }
    }

    int get(int v, int tl, int tr, int pos) {
        if (tl == tr)
            return t[v];
        int tm = (tl + tr) / 2;
        if (pos <= tm)
            return t[v] + get(v*2, tl, tm, pos);       //adding additional values added during updation
        else
           return t[v] + get(v*2+1, tm+1, tr, pos);
    }
```

2. ASSIGNMENT ON SEGMENTS:
---
  -> assign each element of a certain segment a[l...r] to some value p.\
  -> lazy update: instead of changing all segments in the tree that cover the query segment, we only change some and leave others unchanged.\
  -> marked vertex: every element of the corresponding segment is assigned to that value (actually the complete subtree should only contain this value but we are lazy and delay writing the new values to all those vertices)\
  -> this lazy update will lead to some parts of the tree become irrelevant\
  -> for ex
  > query 1: assign x to whole array a[0...n-1] \
          -> x is placed in the root of the tree and this vertex gets marked\
    query 2: assign y to first half of the array a[0...n/2]\
          -> must assign left child of root this number\
          -> but first we have to sort out root vertex first\
          -> also right half must be assigned x but no such information exists there\
    solution: push the info of root to its children then assign children acccording to the latest query, remove the mark from the root\
              -> now we can assign left child with new value without loosing any necessary information
    
   
   -> for any query (modification/reading) during the descent along the tree we should always push information from the current vertex into both of its children i.e. we apply delayed modification but exactly as much as necessary (so not to degrade O(log n) complexity)
    
```cpp
void push(int v) {
    if (marked[v]) {
        t[v*2] = t[v*2+1] = t[v];
        marked[v*2] = marked[v*2+1] = true;
        marked[v] = false;
    }
}

void update(int v, int tl, int tr, int l, int r, int new_val) {
    if (l > r) 
        return;
    if (l == tl && tr == r) {
        t[v] = new_val;
        marked[v] = true;
    } else {
        push(v);
        int tm = (tl + tr) / 2;
        update(v*2, tl, tm, l, min(r, tm), new_val);
        update(v*2+1, tm+1, tr, max(l, tm+1), r, new_val);
    }
}

int get(int v, int tl, int tr, int pos) {
    if (tl == tr) {
        return t[v];
    }
    push(v);                         //here instead of making delayed updates just the value t[v] if marked[v] is true
    int tm = (tl + tr) / 2;
    if (pos <= tm) 
        return get(v*2, tl, tm, pos);
    else
        return get(v*2+1, tm+1, tr, pos);
}
```

3. ADDING ON SEGMENTS, QUERYING FOR MAXIMUM:
---
  
  -> store an additional value for each vertex which stores the addends we haven't propagated to the child vertices. \
  -> before traversing to a child vertex, we call push and propagate the value to both children (both in update and query function)
    
```cpp
void push(int v) {
    t[v*2] += lazy[v];
    lazy[v*2] += lazy[v];
    t[v*2+1] += lazy[v];
    lazy[v*2+1] += lazy[v];
    lazy[v] = 0;
}

void update(int v, int tl, int tr, int l, int r, int addend) {
    if (l > r) 
        return;
    if (l == tl && tr == r) {
        t[v] += addend;
        lazy[v] += addend;
    } else {
        push(v);
        int tm = (tl + tr) / 2;
        update(v*2, tl, tm, l, min(r, tm), addend);
        update(v*2+1, tm+1, tr, max(l, tm+1), r, addend);
        t[v] = max(t[v*2], t[v*2+1]);
    }
}

int query(int v, int tl, int tr, int l, int r) {
    if (l > r)
        return -INF;
    if (l <= tl && tr <= r)
        return t[v];
    push(v);
    int tm = (tl + tr) / 2;
    return max(query(v*2, tl, tm, l, min(r, tm)), 
               query(v*2+1, tm+1, tr, max(l, tm+1), r));
}
```

  
    
