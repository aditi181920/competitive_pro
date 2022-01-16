**There are some loop formations which look like they may take a lot of time but actually they are in bounds**\

1. **Looping over all elements on their multiples:**
```cpp
    for (int i=n;i>=1;i--){
      for(int j=i;j<=n;j+=i){
        ......
        }
    }
```
This actually forms a harmonic progression:\
the pattern of number of times inner loop runs is:\
n+n/2+n/3+n/4+n/5+n/6+.....+n/n\
n(1+1/2+1/3+1/4+1/5+....+1/n)\
slightly greater than nlogn but enough to pass for n<=1e6
