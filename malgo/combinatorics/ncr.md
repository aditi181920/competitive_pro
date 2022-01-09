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
-> though binary exponentiation has a complexity of logn which should be fast enough but in some cases this can lead to a high constant factor making it slow\
-> in such cases we must use third way to find modular inverse which takes O(n)  time for preprocessing but can be answered in O(1)
```cpp
//const ll mod=1000000007;
const ll mod=998244353;
//const ll mod=1000000000;
ll f[100000];
ll inv[100000];
ll finv[100000];
void fact(ll n){
	f[0]=1;
	f[1]=1;
	inv[1]=1;
	finv[0]=finv[1]=1;
    for(int i=2;i<1e5;i++){
		f[i]=(f[i-1]*i);
		f[i]%=mod;
		inv[i]=mod-(mod/i)*inv[mod%i]%mod;
		finv[i]=finv[i-1]*inv[i];
		finv[i]%=mod;
    }
}
ll ncr(ll n, ll r){
	if(n<r || n<0 || r<0)return 0;
	if(n==0 && r==0)return 1;
	ll ans= f[n]*finv[r];
	ans%=mod;
	ans*=finv[n-r];
	ans%=mod;
	//cout<<"ans:"<<ans<<"\n";
	return ans;
}
```
