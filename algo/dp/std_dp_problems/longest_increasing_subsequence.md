**LONGEST INCREASING SUBSEQUENCE/LONGEST STRICTLY INCREASING SUBSEQUENCE:**
--

**Time Complexity:** O(nlogn)

Idea:
-> Traverse every element and for every element find its suitable position in current LIS found


**IMPLEMENTATION:**
--

```sh
  vector<int> lis, pref(n);
	for (int i = 0; i < n; i++) {
		auto it = lower_bound(all(lis), v[i]) - lis.begin();
		if (it == lis.size()) lis.push_back(v[i]);
		else lis[it] = v[i];
		pref[i] = lis.size();
	}
 
-> finding LIS till every i
Note: This is strictly increasing subsequence
For finding increasing subsequence take upper_bound instead of lower_bound and we are done
```

