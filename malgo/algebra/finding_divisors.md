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
IMPLEMENTATION 1:

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

```cpp
IMPLEMENTATION 2:

for(int l:v)
{
  if(l*l>x)   // since if the number is less than sq. of current prime(which will be the smallest prime among the ones left)
	break;    //then this implies there is only 1 prime left 
  if(x%l==0)
  {
	int num=0;
	while(x%l==0)
	{
		num++;
		x/=l;
	}
	a[i].push_back({l,num});
 }
}
```
