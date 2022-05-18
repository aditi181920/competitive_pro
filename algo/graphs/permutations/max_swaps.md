**Given a permutation dearrange it in such a way that it takes max swaps to come back**
--

**Observation:**
--

-> if we have a sorted array we need to just shift it by freq of highest occuring element\
-> now if the array is not sorted we can first sort the array along with every elements old position\
-> after sorting we can map element\
-> now these mapped elements go to old position of the elements they were mapped to \
-> now what if some freq to number comes more than n/2 times\
-> then we can't map exceeding freq to distinct numbers\
-> we keep exceeding freq as it is and work with rest of the numbers


**PROBLEM LINK:**
--

CF GLOBAL 20 F1 (https://codeforces.com/problemset/problem/1672/F1)
