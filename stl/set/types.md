1. **std::set\std::multiset**\
-> implemeted on red black tree\
-> search, removal, insertion has logarithmic time complexity
-> O(log n)

2. **std::unordered_set\std::unordered_multiset**\
-> implemented on hash table\
-> have an avg constt time complexity\
-> but in worst case can be linear if number of collisions become very large\
-> O(1) - O(n)\
-> also modifying values here may corrupt the hash values (have never seen such a things though)(for set)
-> iteration order is not defined therefore cannot use functions like std::equal

Note: set does not support random access iterators therefore functions that operate optimally in worst case using random access iterators will perform linearly in worst case
