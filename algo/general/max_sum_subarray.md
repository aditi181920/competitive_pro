**MAXIMUM SUM SUBARRAY**
--
**COMPLEXITY:** O(n)
  
**Case I:** Only non-negative numbers \
-> Then this problem can be solved easily using sliding window technique only.
  
**Case II:** Negative numbers allowed\
->Then Kadane's algorithm finds it efficiently\
-> The algo says:\
--> Any max subarray will end at some position i in the array. We take advantage of this property of come up with algo idea\
--> At some index i we already know max subarray finishing at i-1 so ending at i will be a[i] or ending at i-1 + a[i]
```cpp

    int best = 0, sum = 0;
    for (int k = 0; k < n; k++) {
    sum = max(array[k],sum+array[k]);
    best = max(best,sum);
    }
    cout << best << "\n";

```
  
