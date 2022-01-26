**GENERAL COMPLEXITIES:**
--

1. **s=s+"xy"; or s+="xy";**\
--> s = s+"xy" creates a copy of s appends "xy" then assigns back to s\
--> Time complexity becomes O(n)\
--> s+=xy just appends "xy" so \
--> Time complexity becomes amortized O(1)

2. **
