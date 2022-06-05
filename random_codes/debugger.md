**SOME RANDOM DEBUGGING TEMPLATE:**
--

Dunno what this does ;((
  
```cpp

// //----------debugger
#ifndef ONLINE_JUDGE
#define debug(x) cerr << #x <<" "; _print(x);
#else
#define debug(x)
#endif
template<class T> void _print(vector<T> arr){
    cerr<<"[ ";
    for(auto x : arr){
        cerr<<x<<" ";
    }
    cerr<<"]";
    cerr<<"\n";
}

template<class T , class V> void _print(map<T , V> mp){
    cerr<<"{ \n";
    for(auto x : mp){
        cerr<<"\t"<<x.first<<" : "<<x.second<<"\n";
    }
    cerr<<"}";
    cerr<<"\n";
}

template<class T , class V> void _print(unordered_map<T , V> mp){
    cerr<<"{ \n";
    for(auto x : mp){
        cerr<<"\t"<<x.first<<" : "<<x.second<<"\n";
    }
    cerr<<"}";
    cerr<<"\n";
}

template<class T , class V> void _print(pair<T , V> p){
    cerr<<"{ "<<p.first<<" "<<p.second<<" }"<<"\n";
}

template<class T> void _print(T x){
    cerr<<x<<"\n";
}

```
