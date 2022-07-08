**2-POINTERS:**
--

-> In this technique we initialize 2 pointers, we keep incrementing the 2nd pointer till the subarray does not satisfy some required condition. As long as it does we can use that subarray, and check for other valid subarray by incrementing the left pointer by 1 and repeating the process

-> This technique is usually used when we have to deal with some subarrays(smallest) that satisfy some condition and the condition is like, if the smallest subarray starting at some index i satisfies it, then any subarray greater than in length starting at index i will satisfy it .
