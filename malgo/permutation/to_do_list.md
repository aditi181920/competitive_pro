

Inversion counting with swap queries in (in each query swap elements at any two indices x and y):\
-> nlogn precomputation with seg tree with a bbst in every node\
-> logn^2 per query \
We perform a range query on the value at index X and the value at index Y to determine the number of numbers smaller than either number in the segment between them, and then compute the change in inversions. After that, we update the 2 indices in the segment tree. Each of the log N nodes takes log N time to update, which gives an overall complexity of log2 N.
from bensonlzl's blog on cf

