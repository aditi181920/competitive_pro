**MAXIMUM SUM SUBSEGMENT OF AN ARRAY:**
--

-> Array contains both positive and negative integers\
-> We need to find a subseg which gives maximum sum of its elements

**APPROACHES:**
--

**1. BRUTE FORCE:**
--

-> Every possible subarray sum 
```cpp
int maxSubArray(vector<int>& nums) {
        int n = size(nums), ans = INT_MIN;
        for(int i = 0; i < n; i++) 
            for(int j = i, curSum = 0; j < n ; j++) 
                curSum += nums[j],
                ans = max(ans, curSum);        
        return ans;
    }

COMPLEXITY: O(n^2)
```

**2. RECURSIVE:**
--

-> every element x belongs to either of the following category:\
1. included in some current running subsegment: next element after x must be either picked further in the recusive tree or the recursion must be stopped\ 
2. not included in some current running subsegment next element after x has two choices either it can be selected for some subsegment or left
```cpp
    int maxSubArray(vector<int>& nums) {    
        return solve(nums, 0, false);
    }
    int solve(vector<int>& A, int i, bool mustPick) {
		// our subarray must contain atleast 1 element. If mustPick is false at end means no element is picked and this is not valid case
        if(i >= size(A)) return mustPick ? 0 : -1e5;       
        if(mustPick)
            return max(0, A[i] + solve(A, i+1, true));                  // either stop here or choose current element and recurse
        return max(solve(A, i+1, false), A[i] + solve(A, i+1, true));   // try both choosing current element or not choosing
    }
COMPLEXITY: O(n^2)(since we will end up examining all possible subarray)
```

**3. MEMOIZATION:**
--

-> there are some repeated states in the above tree as in:
![image](https://user-images.githubusercontent.com/94597499/155286847-80ef88e4-e243-4385-b1d7-6e20e6ba1f6e.png)
```cpp
    int maxSubArray(vector<int>& nums) {    
        vector<vector<int>> dp(2, vector<int>(size(nums), -1));
        return solve(nums, 0, false, dp);
    }
    int solve(vector<int>& A, int i, bool mustPick, vector<vector<int>>& dp) {
        if(i >= size(A)) return mustPick ? 0 : -1e5;
        if(dp[mustPick][i] != -1) return dp[mustPick][i];
        if(mustPick)
            return dp[mustPick][i] = max(0, A[i] + solve(A, i+1, true, dp));
        return dp[mustPick][i] = max(solve(A, i+1, false, dp), A[i] + solve(A, i+1, true, dp));
    }
COMPLEXITY: O(n)(since we calculate for each state exaclty once, n*2 possible states=> n*2 calculation
```

**4. DP:**
--

-> dp[1][i]: maximum subarray sum ending at i (including nums[i])\
-> dp[0][i]: maximum subarray sum upto i (may or may not include nums[i])
```cpp
    int maxSubArray(vector<int>& nums) {
        vector<vector<int>> dp(2, vector<int>(size(nums)));
        dp[0][0] = dp[1][0] = nums[0];
        for(int i = 1; i < size(nums); i++) {
            dp[1][i] = max(nums[i], nums[i] + dp[1][i-1]);
            dp[0][i] = max(dp[0][i-1], dp[1][i]);
        }
        return dp[0].back();
    }
COMPLEXITY: O(n)
```

-> We can actually do away with just 1 row as well.\
-> dp[1][i] : the maximum subarray sum ending at i. \
-> We can just store that row and calculate the overall maximum subarray sum at the end by choosing the maximum of all max subarray sum ending at i.
```cpp
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums);
        for(int i = 1; i < size(nums); i++) 
            dp[i] = max(nums[i], nums[i] + dp[i-1]);        
        return *max_element(begin(dp), end(dp));
    }
COMPLEXITY: O(n)
```

**5. KADANE'S ALGORITHM:**
--

-> From previous approaches we can see that dp[i] only depends on dp[i-1]\
-> Also we can observe that we don't actually need to store complete dp table we can just update max using max sum reached after every iteration
```cpp
    int maxSubArray(vector<int>& nums) {
        int curMax = 0, maxTillNow = INT_MIN;
        for(auto c : nums)
            curMax = max(c, curMax + c),
            maxTillNow = max(maxTillNow, curMax);
        return maxTillNow;
    }

    int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        ll mxsum=-1e12;
        ll sum=0;
        for(int i=0;i<n;i++){
            if(sum<0){
                sum=nums[i];
            }else{
                sum+=nums[i];
            }
            mxsum=max(mxsum,sum);
        }
        return mxsum;
        
    }

COMPLEXITY: O(n)
```

**6. DIVIDE AND CONQUER:**
--

-> the maximum subarray sum is such that it lies somewhere \
---> entirely in the left-half of array [L, mid-1], OR\
---> entirely in the right-half of array [mid+1, R], OR\
---> in array consisting of mid element along with some part of left-half and some part of right-half such that these form contiguous subarray - [L', R'] = [L', mid-1] + [mid] + [mid+1,R'], where L' >= L and R' <= R\
With the above observation, we can recursively divide the array into sub-problems on the left and right halves and then combine these results on the way back up to find the maximum subarray sum.

```cpp
int maxSubArray(vector<int>& nums) {
        return maxSubArray(nums, 0, size(nums)-1);
    }
    int maxSubArray(vector<int>& A, int L, int R){
        if(L > R) return INT_MIN;
        int mid = (L + R) / 2, leftSum = 0, rightSum = 0;
        // leftSum = max subarray sum in [L, mid-1] and starting from mid-1
        for(int i = mid-1, curSum = 0; i >= L; i--)
            curSum += A[i],
            leftSum=max(leftSum, curSum);
        // rightSum = max subarray sum in [mid+1, R] and starting from mid+1
        for(int i = mid+1, curSum = 0; i <= R; i++)
            curSum += A[i],
            rightSum = max(rightSum, curSum);        
		// return max of 3 cases 
        return max({ maxSubArray(A, L, mid-1), maxSubArray(A, mid+1, R), leftSum + A[mid] + rightSum });

COMPLEXITY: O(nlogn)
```

**7. OPTIMIZED DIVIDE AND CONQUER:**
---

-> The O(n) time consumed in combining can be brought down to O(1) if we do some preprocessing\
-> pre[i] : maximum sum subarray ending at i \
-> suf[i] : maximum subarray starting at i
```cpp
vector<int> pre, suf;
    int maxSubArray(vector<int>& nums) {
        pre = suf = nums;
        for(int i = 1; i < size(nums); i++)  pre[i] += max(0, pre[i-1]);
        for(int i = size(nums)-2; ~i; i--)   suf[i] += max(0, suf[i+1]);
        return maxSubArray(nums, 0, size(nums)-1);
    }
    int maxSubArray(vector<int>& A, int L, int R){
        if(L == R) return A[L];
        int mid = (L + R) / 2;
        return max({ maxSubArray(A, L, mid), maxSubArray(A, mid+1, R), pre[mid] + suf[mid+1] });
    }	
COMPLEXITY: O(n)
```
-> But this is kinda overkill because after computing pre we can find max subaaray from that only 


**PROBLEMS:**
--

[EDU 123 DIV2](https://codeforces.com/contest/1644/problem/C)
