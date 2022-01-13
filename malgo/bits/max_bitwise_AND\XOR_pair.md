**MAXIMUM AND VALUE OF A PAIR IN AN ARRAY:**
--

-> Will start from the highest bit and check if atleast 2 numbers have the that bit+bits already included into ans set \
--> if yes then add that bit value into ans\
--> if not then can't take that bit

**MAXIMUM XOR VALUE OF A PAIR IN AN ARRAY:**
--

-> we change the statement a bit:\
-> we find 2 numbers in an array, such that xor of which equals a number x where x will be the max number we want to achieve till ith bit:\
-> the idea is somewhat similar to the previous idea \
-> let's say at some position we have found the highest value to be x then if we want to check if the current bit can be taken or not\
-> we can check that bit value+ x value equals to xor of some 2 numbers given that bits preceeding current bit including it is as it is rest set to 0 using mask

**IMPLEMENTATION:**
--

```cpp
#include <bits/stdc++.h>
using namespace std;
// Function to return the
// maximum xor
int max_xor(int arr[], int n)
{
    int maxx = 0, mask = 0;
    set<int> se;
    for (int i = 30; i >= 0; i--) {
        // set the i'th bit in mask
        // like 100000, 110000, 111000..
        mask |= (1 << i);
        for (int i = 0; i < n; ++i) {
            // Just keep the prefix till
            // i'th bit neglecting all
            // the bit's after i'th bit
            se.insert(arr[i] & mask);
        }
        int newMaxx = maxx | (1 << i);
        for (int prefix : se) {
            // find two pair in set
            // such that a^b = newMaxx
            // which is the highest
            // possible bit can be obtained
            if (se.count(newMaxx ^ prefix)) {
                maxx = newMaxx;
                break;
            }
        }
        // clear the set for next
        // iteration
        se.clear();
    }
    return maxx;
}

// Driver Code
int main()
{
    int arr[] = { 25, 10, 2, 8, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << max_xor(arr, n) << endl;
    return 0;
}
```
