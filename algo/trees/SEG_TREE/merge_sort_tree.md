**MERGE_SORT_TREE:**
--

-> It is just normal segtree but every vertex contains the list of elements belonging to that segment\
-> This consumes O(nlogn) memory since we have logn levels and at each level every element is being used once\
-> adv? we can jump to required segments and do binary search easily on the list of elements\



-> Some modification of this is maintaining a multiset instead of vector at each node\
-> With vector we can;t do efficient updates but with multiset we can but multiset will require logn extra factor in O(nlogn) creation time making it O(nlog^2)
