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
ll f[100000000];
void fact(ll n){
	f[0]=1;
	f[1]=1;
    for(int i=2;i<1e8;i++){
		f[i]=(f[i-1]*i);
		f[i]%=mod;
    }
}
ll exp(ll n,ll p){
    ll ans=1;
	n%=mod;
	if(p==0)return 1;
	if(p==1)return n;
    while(p>0){
        if(p&1){
			ans*=n;
			ans%=mod;
        }
		n*=n;
		n%=mod;
        p>>=1;
    }
    return ans;
}
ll ncr(ll n, ll r){
	if(n<r || n<0 || r<0)return 0;
	if(n==0 && r==0)return 1;
	ll ans= f[n]*exp(f[r],mod-2);
	ans%=mod;
	ans*=exp(f[n-r],mod-2);
	ans%=mod;
	//cout<<"ans:"<<ans<<"\n";
	return ans;
}
```
