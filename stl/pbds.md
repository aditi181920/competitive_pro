**HEADER FILES:**
--
-> #include <ext/pb_ds/assoc_container.hpp> // Common file\
-> #include <ext/pb_ds/tree_policy.hpp> // Including tree_order_statistics_node_update\
-> #include <ext/pb_ds/detail/standard_policies.hpp> //this header file just includes above both header files\
-> **namespace:**\
---> pb_ds //for older versions of C++\
---> gnu_pbds //for newer versions of C++

**DECLARATION:**
--
    template<
	  typename Key, // Key type
	  typename Mapped, // Mapped-policy
	  typename Cmp_Fn = std::less<Key>, // Key comparison functor
	  typename Tag = rb_tree_tag, // Specifies which underlying data structure to use
	  template<
	  typename Const_Node_Iterator,
	  typename Node_Iterator,
	  typename Cmp_Fn_,
	  typename Allocator_>
	  class Node_Update = null_node_update, // A policy for updating node invariants
	  typename Allocator = std::allocator<char> > // An allocator type
	  class tree;

-> initializing the template to only the first two type will leave us with a map
-> tag and node_update are missing in map

**VALUES FOR ARGUMENTS:**
--

1. **2nd TYPENAME ARGUMENT:**\
 --> mapped : map implemetation\
 --> null_type : set implementation
 
2. **Tag:**\
 -> denotes tree structure that will be used\
 -> three base classes provided for this in STL are :\
 --->  rb_tree_tag (red-black tree)\
 ---> splay_tree_tag (splay tree)\
 ---> ov_tree_tag (ordered-vector tree)\
 -> at competitions we can use only red-black trees for this because splay tree and OV-tree using linear-timed split operation that prevents us to use them.
 
3. **Node update:**\
 -> class denoting policy for updating node invariants\
 -> policies available:\
 ---> null_node_update, ie, additional information not stored in the vertices.\
 ---> tree_order_statistics_node_update, which, in fact, carries the necessary operations. 
 
 **TRIVIAL IMPLEMENTATION OF SET:**
 --
 ```sh
 typedef tree<
int,
null_type,
less<int>,
rb_tree_tag,
tree_order_statistics_node_update>
ordered_set;
```
-> changing null_type to map will lead to trivial implemetation of map

**COMPARATOR FUNCTION:**
--
-> to implement a multiset use less_eq<int> comparator\
-> note that using less_eq swaps the functionalities of lower_bound and upper_bound i.e. former will work like latter and vice-versa

**SOME FEATURES:**
--
1. find_by_order() : returns an iterator to the k-th largest element (counting from zero)
2. order_of_key() : the number of items in a set that are strictly smaller than our item. 
