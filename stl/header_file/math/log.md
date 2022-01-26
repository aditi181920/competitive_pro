1. **log()/log10()/log2()**\
-> All these return double data type values so they must be avoided on larger n as to avoid precision error\
-> In log calculation when n increases precision of the calculation decreases

-> A nice hack to find log2() in O(1) time complexity is to use __builtin_clz function to cnt leading bits subtract from total bits to find total number in binary representation and then subtract 1 to get highest power of binary representation which will be the req log value(in int of course)
```sh

int log(long long x)
{
    return 64 - __builtin_clzll(x) - 1;
}
```
