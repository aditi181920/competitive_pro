**SORT()**
--
-> header : <algorithm>\
-> Sorts the elements in the range [first, last) in non-descending order, where first and last are random access iterators\
-> Time Complexity: O(n log n) in worst case\
-> **SYNTAX:** sort(pointer defining start of range, pointer defining end of range, (optional) cmparator)\
-> to sort in decreasing order:

      1. use std::greater in declaration (not done this method ever though, may not work for every container\
      2. use std::greater as third parameter in sort\
      3. define your own comparator function as third parameter in sort
      
 **BINARY_SEARCH()**
 --
 -> header: <algorithm> \
 -> prerequisite: range must be sorted and first and last must be random access iterator\
 -> Checks if an element equivalent to value appears within the range [first, last)\
 -> Time Complexity: O(log n) in worst case
                                                                       
 **LOWER_BOUND()**
 --
 -> header: <algorithm> \
 -> prerequisite: sorted seq \
 -> implemented using binary search\
 -> Returns an iterator pointing to the first element in the range [first, last) that is not less than value, or last if no such element is found\
 -> Time Complexity: O(log n) in worst case
                                                                    
**UPPER_BOUND()**
--
-> header: <algorithm> \
-> prerequisite: sorted seq \
-> implemented using binary search\
-> Returns an iterator pointing to the first element in the range [first, last) that is greater than value, or last if no such element is found\
-> Time Complexity: O(log n) in worst case                                                                       
