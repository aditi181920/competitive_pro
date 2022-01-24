**BINOMIAL PROPERTIES:**
---

1. q(<sup>p</sup> C <sub>q</sub>) = p(<sup>p-1</sup> C <sub>q-1</sub>)\
--> Proof: q can be divided by q! then will get (q-1)! in denominator and multiplying and dividing p will give p.(p-1)!

2. (<sup>p</sup> C <sub>q</sub>) = (<sup> p-1</sup> C <sub>q</sub>)+(<sup>p-1</sup>C<sub>q-1</sub>)\
--> Proof: let's say there is some x belonging to p items then we have 2 options for it : either that will be included in chosen q items so we have to choose q-1 from p-1 now or it will not be choosen then we will have to choose q elements from p-1 other elements

3. (UPPER SUMMATION IDENTITY) summation(m=k to n) (<sup>m</sup> V <sub>k</sub>) = (<sup>n+1</sup> C <sub>k+1</sub>)\
--> Proof: it is just like fix a element then u have choice to pick any element smaller than that \
--> RHS: no. of subsets of {1,...,n+1} of size k+1 counted directly\
--> LHS: for each possible subset size ; specifies largest element in subset say if largest element is k+1 remaining k must be chosen from {1,..,k}, (<sup>k</sup> C <sub>k</sub>) ways; if largest element is k+2, remaining k must be choosen from {1,...k+1}, (<sup>k+1</sup> C <sub>k</sub>) ways

4. (PARALLEL SUMMATION IDENTITY) summation(k=0 to n) (<sup>m+k</sup> C<sub>k</sub>) = (<sup>n+m+1</sup> C<sub>n</sub>)\
--> Proof: RHS : no. of subsets of {1,...,n+m+1} of size n, counted directly\
--> LHS: specifies smallest element no in subset say if smallest missed element is 1, then all n elements must be choosen from {2,...,n+m+1},(<sup>m+n</sup> C <sub>n</sub>) ways, if smallest missed element is 2, then 1 is in the subset and remaining n-1 elements must be chosen from {3,...,n+m+1}, (<sup>m+n-1</sup> C<sub>n-1</sub>) ways

5. (SQUARE SUMMATION IDENTITY) summation(k=0 to n) (<sup>n</sup> C <sub>k</sub>)^2 = (<sup>2n</sup> C <sub>n</sub>)\
--> RHS: no. of subsets of {+1,-1,+2,-2,+3,-3,....,+n,-n} of size n counted directly\
--> LHS: by specifying k choose k positive elements (<sup>n</sup> C <sub>k</sub>) and n-k negative elements ((<sup>n</sup>C<sub>n-k</sub>) = (<sup>n</sup> C<sub>n-k</sub>))

6. (VANDERMONDE IDENTITY) summation(k=0 to r)((<sup>m</sup> C<sub>k</sub>)(<sup>n</sup>C<sub>r-k</sub>)) = (<sup>n+m</sup> C <sub>r</sub>))\
--> Let A={x1,x2,...,xm} and B={y1,y2,...yn} be disjoint set\
--> RHS: no. of subsets of size r, counted directly\
--> LHS: specifies k, the no. of elements chosen from A ((<sup>m</sup> C <sub>k</sub>) ways) and remaining r-k elements from B ((<sup>n</sup> C <sub>r-k</sub>) ways)

7. (GAUSS'S TRICK) summation (r=0 to n) r.(<sup>n</sup> C <sub>r</sub>) = summation(r=0 to n) (n-r)(<sup>n</sup>C <sub>n-r</sub>) \
--> can be proved since binomial coefficients are symmetric

8. summation (k=0 to n) (<sup>n</sup>C<sub>k</sub>) = 2^n
--> becoz this is just choosing all possible subsets
