**DIGIT DP**
---

Digit DP is a technique of DP which helps us solve problems of finding how many numbers between 2 values (say a and b) which satisfy a particular property

**COMPARING NUMBERS:**
--
-> Let's say we have 2 numbers with decimal representation A=a1a2....an and B=b1b2b3...bm\
-> A<B if length of A<length of B or ai=bi from left to right until there is a digit ai<bi and then digits yi can have values [0-9] for j>i

**EXAMPLE 1:**
--
**1. STATEMENT:**
--
Cnt no.'s x in range a to b such that digit d occurs exactly k times in x 

**2. BUILDING THE SEQ:**
--
-> Let's say during the building of the seq, currently we are at the position pos and have already placed some digits in position from 1 to pos-1.\
-> If there exists any t (1<=t<pos) where sq[t]<b[t](b is the upper bound number here) then we can place any digit in our current position because the seq will be small no matter what we place\
-> But if there was no t that satisfy that condition then we can only place digits smaller than b[pos] there

**3. INFO REQUIRED:**
--
-> Since we only need to whether a valid t exists in the seq we have builded till now so we can pass info by just using a flag\
-> Whenever we place a digit at position t which is smaller than b[t] we can make the flag set for next recursive calls\
-> Now for the condition of digit d occuring exactly k times in the seq we can pass another parameter cnt which cnt's no. of times we have placed digit d so far in our seq and whenever we place digit d in our seq we increment cnt in our next recursive calls\
-> In base case when whole seq is built just check if cnt is eq to d (return 1) or not (return 0)

**4. STATES:**
--
-> 3 states for dp memoization: current pos, if no. has already become smaller than b, freq of digits till now\
-> above approach was finding no's in the range from 0 to b. To find in a to b. ans(0,b)-ans(0,a-1)\
-> we can actually solve a to b in single recursion but we will have to keep info about comparsion of sq[t] with a[t] also
