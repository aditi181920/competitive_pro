**FERMAT'S LITTLE THEOREM:**
```
-> for any integer a and prime p a^(p-1) = 1(mod p)
=> a^(p-2) = a^(-1) (mod p)
```

**nCr CALCULATION USING FERMAT'S LITTLE THEOREM:**
```
 nCr = ((n!)/((r!)(n-r)!)) (mod p)
     = (n! * (r!)^(-1) * ((n-r)!)^(-1)) (mod p)
     = (n! * (r!)^(p-2) * ((n-r)!)^(p-2)) (mod p)
```

**IMPLEMENTATION:**
```cpp
ll fact(ll n){
    ll ans=1;
    for(int i=2;i<=n;i++){
        ans=(ans*i)%mod;
        ans%=mod;
    }
    return ans;
}
ll exp(ll n,ll p){
    ll ans=1;
    while(p){
        if(p&1){
            ans=(ans*n)%mod;
        }
        n=n*n%mod;
        p>>=1;
    }
    return ans;
}
ll ncr(ll tot, ll s){
    return (((fact(tot)%mod)*(exp(fact(s)%mod,mod-2)%mod)%mod)*(exp((fact(tot-s)%mod),mod-2)%mod)%mod);
}
```
