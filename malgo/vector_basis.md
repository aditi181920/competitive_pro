1.  addition and subtraction in modulo 2 arithmetic = xor (since there does not exist any concept of borrow or carry)
2. Z<sub>2</sub>: Z<sub>m</sub> is the set of remainders upon division by m. So, Z<sub>2</sub> is simply the set {0,1}
3. Z<sub>2</sub><sup>d</sup>: A d−dimensional vector space consisting of all the different position vectors that consists of d coordinates, all coordinates being elements of Z<sub>2</sub>
4. xor-operation is equivalent to vector addition in a Z<sub>2</sub><sup>d</sup> vector space.
5. Independent Vectors: A set of vectors v1<sup>→</sup>,v2<sup>→</sup>,…,vn<sup>→</sup> is called independent, if none of them can be written as the sum of a linear combination of the rest.
6. Basis of a Vector Space: A set of vectors is called a basis of a vector space, if all of the element vectors of that space can be written uniquely as the sum of a linear combination of elements of that basis.
7. Any vector in V may be expressed as a linear combination of elements of S in only one way.
8. All possible basis of a vector space will have same number of elements 
9. For a set of independent vectors, we can change any of these vectors by adding to it any linear combination of all of them, and the vectors will still stay independent. The set of vectors in the space representable by some linear combination of this independent set stays exactly the same after the change.
10. Notice that, in case of Z<sub>2</sub><sup>d</sup> vector space, the coefficients in the linear combination of vectors must also lie in Z<sub>2</sub>. Which means that, an element vector can either stay or not stay in a linear combination, there's no in-between.
11. Basis vectors are linearly independent
12. For a d−dimensional vector space, it's basis can have at most d vector elements.
13. A basis of d elements can represent a vector space of 2<sup>d</sup> -1
14. Basis cannot have zero
15. On adding new element to basis, basis size increases by 1 and vector size increases by double the previous size
16. To check if an element belongs to vector space:
--> Since every element of basis has unique msb 
--> in decreasing order of msb iterate the basis
--> if element has set bit but basis does not then insert in basis
--> if there is, subtract corresponding basis element from this (xor) 
```cpp
typedef long long ll; // represents ints in [0,2^{60})
vector<ll> basis; // list of basis elements, initially empty
for (ll a: X) { // go through elements in any order
  ll A = a;
  for (ll b: basis) A = min(A,A^b);
  if (A) { // add A to basis
    int ind = 0;
    while (ind < basis.size() && basis[ind] > A) ind ++;
    basis.insert(begin(basis)+ind,A);
    // preserve decreasing property
  }
}
```
Note that a shorter version exists which works perfectly fine
```cpp
    vector<ll> basis;
    for(ll x:a){
        for(ll b:basis){
            x=min(x,x^b);
        }
        if(x>0){
            basis.push_back(x);
        }
    }
```
17. Finding ith element of vector space from a basis (vector space is in increasing order)
--> A cool trick is:
```cpp
sort(basis.begin(),basis.end());
ll ans=0;
for(ll j=basis.size()-1;j>=0;j--){
    if((i>>j)&1){
        ans=max(ans,ans^basis[j]);
    }else{
        ans=min(ans,ans^basis[j]);
    }
}
```

