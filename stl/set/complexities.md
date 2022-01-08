1. **distance():**
-> best case: O(1) but not for set.. does work for vector and other containers that support random access iterator\
-> worst case: O(n) for set since set does not support random access iterators \
-> alternative: use pbds ordered_set and its functions 

2. **lower_bound()/upper_bound():**
-> again due to absence of support of random access iterator the complexity may be O(n) instead of O(log n)(not very sure though)\
