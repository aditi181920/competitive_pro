**ENUMERATING ALL POINTS IN A PLANE WHICH ARE ATMOST K DISTANCE APART:**
--

Let's say we have two points (xp,yp) and (xq,yq) then we can deduce that:
```sh
       sqrt((xp-xq)^2+ (yp-yq)^2) <= k
       (xp-xq)^2 + (yp-yq)^2 <= k*k
       ((xp-xq)/k)^2 + ((yp-yq)/k)^2 <= 1
        => ((xp-xq)/k)^2 <= 1 && ((yp-yq)/k)^2 <=1
        => -1<= (xp/k - xq/k) <= 1   &&  -1<= (yp/k-yq/k) <= 1
        => if a point is assigned to packet (x,y) then the point to be paired can only be contained in 
            --> the packet itself 
            --> or adjacent packets (x+l,y+m) l=[-1,1] and m=[-1,1]
```
-> this problem has an complexity of O(n+m) where m is the number of points to output  // didn't get this complexity analysis though\
-> we can use map of pair though to maintain collection of points that belong to a coordinate but pairs are slow so we can use an alternative way:\
-> technique to define the packets uniquely is to take an arbitrarily big number which exceeds the constraint of coordinate like:
```sh
   lets say xi lies between [0,1e9] 
   big = 2*1e10  (say)
   map (xi,yi) to value: xi*big+yi , we can collect all points to this map value now 
   also note:
   if just using pairs of (xi/k,yi/k) we can just add values [-1..1,-1..1] and find all possible packets
   but if using a big number technique then the possible backets become:
   ((xi+1)*big)/k+yi = big
   ((xi-1)*big)/k+yi = -big
   ((xi+1)*big)/k+(yi+1) = big+1
   ((xi-1)*big)/k+(yi+1) = -big+1
   ((xi+1)*big)/k+(yi-1) = big-1
   ((xi-1)*big)/k+(yi-1) = -big-1
   (xi*big)/k+(yi+1) = 1
   (xi*big)/k+(yi-1) = -1
   (xi*big)/k+yi = 0
```

**PROBLEM LINK:**
--

[ABC 234 Ex](https://atcoder.jp/contests/abc234/tasks/abc234_h?lang=en)
