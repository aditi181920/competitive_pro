**FINDING DIVISORS OF A NUMBER:**
--

```cpp
vector<int> d;
for(int i=1;i<=sqrt(n);i++){
    if(x%i==0){
      d.push_back(i);
      if((x/i)!=i){
        d.push_back(x/i);
      }
    }
}
```

**FINDING PRIME DIVISORS:**
```cpp
 for(int i=2;i<MAX;i++){
    if(!pf[i].empty()){continue;}    //remember how prime sieve is formulated, the same idea
    for(int j=i;j<MAX;j+=i){
      int mj=j;
      while(mj%i==0){
        pf[j].push_back(i);
        mj/=i;
      }
    }
  }
  MAX: maximum allowable prime factor
```
