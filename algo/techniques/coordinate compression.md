**COORDINATE COMPRESSION:**
--

-> Maps have too big complexity , this is generally used when we need to count things which can have very large value but storing space is less so we can compress those values down to storage space\
-> Note that manipulating values must not affect the result 

```cpp

struct custom_hash {
    static uint64_t splitmix64(uint64_t x) {
        // http://xorshift.di.unimi.it/splitmix64.c
        x += 0x9e3779b97f4a7c15;
        x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9;
        x = (x ^ (x >> 27)) * 0x94d049bb133111eb;
        return x ^ (x >> 31);
    }
 
    size_t operator()(uint64_t x) const {
        static const uint64_t FIXED_RANDOM = chrono::steady_clock::now().time_since_epoch().count();
        return splitmix64(x + FIXED_RANDOM);
    }
};
int main(){
    unordered_map<ll,ll, custom_hash> comp; 
    int n;
    cin>>n;
    ll a[n+1];
    vector<ll> nums(n),cnt(n+1);
    for(int i=1;i<=n;i++){
      cin>>a[i];
      nums[i-1]=a[i];
    }
    nums.resize(unique(nums.begin(),nums.end())-nums.begin());
    for(int i=1;i<=nums.size();i++){
      comp[nums[i-1]]=i;
    }
    for(int i=1;i<=n;i++){
      a[i]=comp[a[i]];
    }
}
```
