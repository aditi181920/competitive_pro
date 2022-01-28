**GIVEN AN ARRAY FIND [X,Y] AND PARITION IT IN K SEGMENTS SUCH THAT IN EACH SEGMENT NO. OF ELEMENTS BELONGING TO [X,Y] IS STRICTLY GREATER THAN NUMBER OF THOSE NOT BELONGING TO. YOU ALSO HAVE TO MINIMIZE Y-X**
---

**OBSERVATIONS:**
--

-> Lets say we have a found [x,y] then when it will be valid?\
--> if we have k segments then in each segment n(in range)>n(outside range)\
--> ==> for whole array n(in range)-n(outside range) >=k then we can always divide it in k segments \
-> we can denote number belonging to range by 1 and not belonging by -1 then by just taking sum we can find out whether it is valid or not\
-> now how to find optimal [x,y] out of all valid [x,y]'s?\
-> we have 2 ways:\
---> we can just do a binary search on y for each x (since each element is upto 1e5 binary search will work well; we can even optimize by using upperbound lowerbound function to find inrange cnt instead of iterating all elements)\
---> we can use two pointers ; keep cnt of every number ; itialize sum with -n(none belongs to range so all -1), now start increasing y and add +2\*cnt[y](parity change) as soon as sum>=k that is when we got the smallest y for that x; just like this we can find for all x;

**PROBLEM LINK:**
--

[CF 768](https://codeforces.com/contest/1631/problem/D)
