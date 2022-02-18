**EVENT METHOD:**
--

-> Given some n events such that they start at li and end at ri. We have to find all intersection of these events and do some operations/find something

**METHOD:**
--

-> We keep all the events in sorted order.\
-> Then we keep track of things that have started but not yet completed

**IMPLEMENTATION:**
--

-> We can keep a set of arrival and departure of current ongoing events and can easily do adding and removing\
-> if index does not matter we can just keep them in one list and process them linearly after sorting\
-> we can keep different vectors of arrival and departure sorted and use two pointers just like merge process of merge sort

**PROBLEM LINKS:**
--

[CF 672 D](https://codeforces.com/contest/1420/problem/D)
