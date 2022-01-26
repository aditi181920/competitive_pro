**GENERAL COMPLEXITIES:**
--

1. **s=s+"xy"; or s+="xy";**\
--> s = s+"xy" creates a copy of s appends "xy" then assigns back to s\
--> Time complexity becomes O(n)\
--> s+=xy just appends "xy" so \
--> Time complexity becomes amortized O(1)

2. **concatenating string is linear in length:**
```
  std::string a;
    for (int i = 0; i < N; ++i) {
      a = a + "xy";
    }                           COMPLEXITY: O(N^2)
    
   std::string a;
    for (int i = 0; i < N; ++i) {
      a = std::move(a) + "xy";           //here memory resources of a are reused and "xy" will just be appended
    }                            COMPLEXITY: O(N)
    
    for adding in beginning :
    s.insert(s.begin(), c) this just takes linear time
    moving or making a copy will just have same complexity 
    
```
SOURCE: [this](https://codeforces.com/blog/entry/66660)
    
    
