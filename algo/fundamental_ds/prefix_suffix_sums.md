**PREFIX/SUFFIX SUMS:**
--

-> Just like we use this concept in arrays, we can use this concept in a matrix which involves contructing some continuous patterns \
-> What we wan do is \
-> Keep a vertical , diag matrix\
-> We initialize vertical prefix arrays in every column in vertical and initialize similarly for digaonal\
-> then we can do vertical prefix sums on every column in vertical and simialrly in diagonal \
-> Now we can merge these two arrays -> the merged array should come out to be like initialized horizontal prefix arrays\
-> The we can just do horizontal prefix sum on all rows and we are done\
-> Note that digonal can be some diagonal pattern which we can make work like normal prefix array using some pattern... it does not need to be perfect digaonal

**PROBLEM:**
--

[ABC 260 G](https://atcoder.jp/contests/abc260/editorial/4466)
