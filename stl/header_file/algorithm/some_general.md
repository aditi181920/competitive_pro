1. **unique()**\
->``` Eliminates all except the first element from every consecutive group of equivalent elements from the range [first, last)```
and returns a past-the-end iterator for the new logical end of the range.\
-> it ```cannot alter the properties of the object``` containing the range of elements (i.e., it cannot alter the size of an array or a container):\
The removal is done by ```replacing the duplicate elements by the next element that is not a duplicate```, and signaling the new size of the shortened range by 
returning an iterator to the element that should be considered its new past-the-end element.\
-> **Return value:** An ```iterator to the element that follows the last element not removed.```\
The range between first and this iterator includes all the elements in the sequence that were not considered duplicates.\
-> **SYNTAX:** unique(pointer to first, pointer to end)\
-> **TIME COMPLEXITY:** Linear

2. **reverse()**\
-> Reverses the order of the elements in the range [first, last)\
-> **SYNTAX:** unique(pointer to first, pointer to end)\
-> **TIME COMPLEXITY:** Linear


