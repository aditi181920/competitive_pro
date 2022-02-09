**MO'S ALGORITHM:**
--

-> this is basically just a way of reordering things to solve range queries such that complexity O(n^2) reduces down to O(n\*sqrt(n))\
-> offline algorithm\
-> Complexity: O((n+q)\*sqrt(n))

**ALGORITHM:**
--

-> We divide input array into sqrt(n) blocks\
-> We order them by ascending order of block numbers of l, and ascending order of r in same blocks for l\
-> now we can just add and remove elements in the current segment to make it equal to the query segment\
-> note becoz of the ordering: now in every block right pointer has to move n total steps in worst case, since there are sqrt(n) blocks so total movement is n\*sqrt(n) as for left pointer in every block atmost sqrt(n) and q queries if in worst case all diff blocks then q\*sqrt(n)\
-> another very significant improvement of this algorithm is :

**IMPORTANT:**\
-> Instead of every right pointer in increasing order in blocks, we make it alternating so that redundant moves are reduced\
-> as for ex: in first block if right pointer reaches n and in second block if it starts from very beginnning coming close to n again then we will go back and come back.... rather we can reduce this redundancy by just going back this 2nd block then coming in 3rd block:)))\
-> block size of sqrt(n) does not always offer best runtime, u may need to increase or decrease blocksize for adjusting run time in some cases\
-> also make the block size defined as const as division by const is well optimized by compilers


**SAMPLE COMPARATOR:**
--

```cpp
bool cmp(array<int,3>x,array<int,3>y)
{
	if(x[0]/N==y[0]/N)
	{
		if((x[0]/N)&1)
			return x[1]>y[1];
		else
			return y[1]>x[1];
	}
	return x[0]<y[0];
}
```

**PROBLEM LINKS:**
---
[ABC 238 G](https://atcoder.jp/contests/abc238/tasks/abc238_g?lang=en)
