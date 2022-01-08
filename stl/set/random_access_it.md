
1. **distance():**
-> best case: O(1) containers that support random access it\
-> worst case: O(n) for set since set does not support random access iterators \
-> alternative: use pbds ordered_set and its functions, it will give O(log n) complexity

2. **lower_bound()/upper_bound():**\
   Note: there are 2 types of lower_bound() and upper_bound() functions
   1. *generic upper_bound:*\
   **SYNTAX:** upper_bound(pointer indicating start position, pointer indicating end position, int val)\
   this works optimally for containers supporting random access it giving O(log n) in worst case\
   but works in linear time O(n) for containers like set that don't support random access iterator\
   [gnereic lower_bound is analogous]
   2. *upper_bound for set:*\
    **SYNTAX:** std::set.upper_bound(int val) \
    this works optimally in O(log n) for sets as this has been implemented so that it works in a optimal way for set
    [lower_bound for set is analogous] 
  
3. **sort():**\
-> Sorts the elements in the range [first, last) in non-descending order, where first and last are random access iterators\
-> Worst complexity: O(nlog n) with random access iterators\
-> to sort in descending order : either use std::greater in the declaration / define your own comparator function

4. **binary_search():**\
-> range [first,last) here first and last should be random access iterators\
-> worst case with random access operator: O(log n)


