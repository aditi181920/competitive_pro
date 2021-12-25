TERNARY SEARCH
---
COMPLEXITY: O(LOG3N)+4

   **PREREQUISITES:** \
   ->applied on unimodal functions, i.e. \
   --> functions that strictly increases first, reaches a maximum and then strictly decreases \
   --> functions that strictly decreases first, reaches a minimum and then strictly increases \
   ->both above cases are symmetric, we'll discuss the first case
   
   ---
   
   **ALGORITHM:** \
   Let m1 and m2 be two pts s.t. l<m1<m2<r. We'll end up at 3 cases:\
   -> f(m1)<f(m2)\
      either m1 or both m1 and m2 lie on the increasing side of the function, so we know for sure that the function does not lie in interval [l,m1]\
      so we have to search for the max in the seg [m1,r]\
   -> f(m1)>f(m2)\
      either m2 or both m1 and m2 lie on the decreasing side of the function, so we know for sure that the function does not lie in interval [m2,r]\
      so we have to search for the max in the seg [l,m2]\
   -> f(m1)==f(m2)\
      both m1 and m2 are maximized, so search space reduces to [m1,m2] as both points must lie on opp sides so maxima will lie in between
   
   The most common way is to choose the points so that they divide the interval [l,r] into three equal parts.\
   m1=l+(r−l)/3 \
   m2=r−(r−l)/3
   
   NOTE: When (r-l)<3 then ternary search must stop as , l,r,m1,m2 can no longer be pairwise distinct so we may end up in an infinite loop. So when such condition is encountered
   we must check r,l,m1,m2 values and find the max
   ```cpp
   double ternary_search(double l, double r) {
    double eps = 1e-9;              //set the error limit here
    while (r - l > eps) {
        double m1 = l + (r - l) / 3;
        double m2 = r - (r - l) / 3;
        double f1 = f(m1);      //evaluates the function at m1
        double f2 = f(m2);      //evaluates the function at m2
        if (f1 < f2)
            l = m1;
        else
            r = m2;
    }
    return f(l);                    //return the maximum of f(x) in [l, r]
    }
   
   //can change the implementation a little using the note above 
 ```
 
   
