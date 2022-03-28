**FIND VERTICES THAT LEAD TO DIRECTED CYCLES:**
--

We can easily do this by noticing that given a directed graph initailly vertices having zero outdegree will never be part of our answer\
Now we can just remove the contribution of outdegree by these vertices and see if we obtain new vertices with zero outdegree and so on\
Since these vertices lead to only non-cycle vertices so these can't be part of our answer either\
In the end we will only be left with required vertices


**PROBLEM LINK:**
--

[ABC 245 F] (https://atcoder.jp/contests/abc245/tasks/abc245_f)
