**SUB MATRIX SUM:**
--

-> Given a matrix we want to find sum of its submatrices:\
-> for that we first need to follow the below steps:
```cpp
   -> find the sum of all submatrics s.t.:

      a[i+1][j+1] = sum of submatrix (0,0) to (i,j)
        
   -> now using a we can find sum of any submatrix 
   -> let's say we want to find sum of submatrix of size [h,w] from some index(i,j)
        ---> i.e. submatrix (i,j) (i-h,j-w) :

        int x = i+1-h, y=j+1-w;
        a[i+1][j+1]-a[x][j+1]-a[i+1][y]+a[x][y]
        
```

**PROBLEM LINKS:**
--
[BIWEEKLY 69 D](https://leetcode.com/contest/biweekly-contest-69/problems/stamping-the-grid/)
