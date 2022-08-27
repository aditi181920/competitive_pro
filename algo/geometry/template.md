```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define ld long double
#define mp make_pair
#define fast_io ios::sync_with_stdio(0);cin.tie(0); cout.tie(0);
//-----constants---------------
ll llmx=1e15;
ll llmn=-1e15;
const ll mod =998244353;
//const ll mod=1000000007;
const int N = 5e5 + 5;
const int SN = 1 << 20;
const long long inf = 1e16 + 16;
//-----containers--------------
template <typename T> T pythag(T a,T b){  //returns x= a*a+ b*b
  return hypot(a,b);
}
template <typename T> T fndangle(T a, T b){
  return atan2(b,a);
}
template <typename T> T degtorad(T a){
  return (a*3.1415926535)/180;
}
pair<ld,ld> polar(ld rad,ld theta){
  return {rad*cos(theta),rad*sin(theta)};
}
```
