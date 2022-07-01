**Cool techniques for dp on tree problems:**
--

**Combinatorial:**
--

-> Say u need to count some number of ways that satisfy some constaint in the tree. The trick is we calculate for leaves trivially and then when we go up.. if total ways for some child (without considering the conditions in problem) is x , then we say ok it is not x but dp[x] so remove x from total ways and multiply dp[x] and similarly we do this for all the childs\


**PROBLEM:**
--
[ABC 160 F](https://atcoder.jp/contests/abc160/tasks/abc160_f?lang=en)
