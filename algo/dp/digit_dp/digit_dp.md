**DIGIT DP**
---

Digit DP is a technique of DP which helps us solve problems of finding how many numbers between 2 values (say a and b) which satisfy a particular property

**COMPARING NUMBERS:**
--
-> Let's say we have 2 numbers with decimal representation A=a1a2....an and B=b1b2b3...bm\
-> A<B if length of A<length of B or ai=bi from left to right until there is a digit ai<bi and then digits yi can have values [0-9] for j>i

**EXAMPLE 1:**
--
**1. STATEMENT:**
--
Cnt no.'s x in range a to b such that digit d occurs exactly k times in x 

**2. BUILDING THE SEQ:**
--
-> Let's say during the building of the seq, currently we are at the position pos and have already placed some digits in position from 1 to pos-1.\
-> If there exists any t (1<=t<pos) where sq[t]<b[t](b is the upper bound number here) then we can place any digit in our current position because the seq will be small no matter what we place\
-> But if there was no t that satisfy that condition then we can only place digits smaller than b[pos] there

**3. INFO REQUIRED:**
--
-> Since we only need to whether a valid t exists in the seq we have builded till now so we can pass info by just using a flag\
-> Whenever we place a digit at position t which is smaller than b[t] we can make the flag set for next recursive calls\
-> Now for the condition of digit d occuring exactly k times in the seq we can pass another parameter cnt which cnt's no. of times we have placed digit d so far in our seq and whenever we place digit d in our seq we increment cnt in our next recursive calls\
-> In base case when whole seq is built just check if cnt is eq to d (return 1) or not (return 0)

**4. STATES:**
--
-> 3 states for dp memoization: current pos, if no. has already become smaller than b, freq of digits till now\
-> above approach was finding no's in the range from 0 to b. To find in a to b. ans(0,b)-ans(0,a-1)\
-> we can actually solve a to b in single recursion but we will have to keep info about comparsion of sq[t] with a[t] also

**5. IMPLEMENTATION:**
--
```cpp
/// How many numbers x are there in the range a to b, where the digit d occurs exactly k times in x?

#include <bits/stdc++.h>
using namespace std;

vector<int> num;
int a, b, d, k;
int DP[12][12][2];
/// DP[p][c][f] = Number of valid numbers <= b from this state
/// p = current position from left side (zero based)
/// c = number of times we have placed the digit d so far
/// f = the number we are building has already become smaller than b? [0 = no, 1 = yes]

int call(int pos, int cnt, int f){
    if(cnt > k) return 0;

    if(pos == num.size()){
        if(cnt == k) return 1;
        return 0;
    }

    if(DP[pos][cnt][f] != -1) return DP[pos][cnt][f];
    int res = 0;

    int LMT;

    if(f == 0){
        /// Digits we placed so far matches with the prefix of b
        /// So if we place any digit > num[pos] in the current position, then the number will become greater than b
        LMT = num[pos];
    } else {
        /// The number has already become smaller than b. We can place any digit now.
        LMT = 9;
    }

    /// Try to place all the valid digits such that the number doesn't exceed b
    for(int dgt = 0; dgt<=LMT; dgt++){
        int nf = f;
        int ncnt = cnt;
        if(f == 0 && dgt < LMT) nf = 1; /// The number is getting smaller at this position
        if(dgt == d) ncnt++;
        if(ncnt <= k) res += call(pos+1, ncnt, nf);
    }

    return DP[pos][cnt][f] = res;
}

int solve(int b){
    num.clear();
    while(b>0){
        num.push_back(b%10);
        b/=10;
    }
    reverse(num.begin(), num.end());
    /// Stored all the digits of b in num for simplicity

    memset(DP, -1, sizeof(DP));
    int res = call(0, 0, 0);
    return res;
}

int main () {

    cin >> a >> b >> d >> k;
    int res = solve(b) - solve(a-1);
    cout << res << endl;

    return 0;
}
```

**EXAMPLE 2:**
---

**1. PROBLEM STATEMENT:**
--
-> Consider the problem of calculating how many integers in the interval [L..R] have sum divisible by a number K.

**IMPLEMENTATION:**
--
```cpp
string tostring(long long n)
{
   string s;
   while(n!=0)
  {
      s+=(n%10)+'0';
      n/=10;
   }
    reverse(s.begin(), s.end());
    return s;
}

long long dp[12][2][83]; //dp[index][smaller][remainder]

//For integers, the sum of digits can't be greater than 82

long long k;

string s;

long long dp_solve(string & s,int index,bool smaller,int mod1)
{
 if(index==s.length())
 {
        if(mod1==0)
        {
            return 1;

         }
     return 0;

 }
  if(dp[index][smaller][mod1]!=-1)
      {
       return dp[index][smaller][mod1];

      }
    else
    {
        int limit=9;

        if(smaller)
        {
            limit=s[index]-'0';
        }
        long long init_count=0;

        for(int i=0;i<=limit;i++)
        {
            bool ns;
            if(i<s[index]-'0')
            {   
                ns=0;
            }
            else
            {
                ns=smaller;
            }

            init_count+=dp_solve(s, index+1, ns,(mod1+i)%k);

        }


        dp[index][smaller][mod1]=init_count;
        return init_count;

    }

}


int main()
{

      int a,b; //Find numbers between A and B whose sum of digits is divisible by K
      cin>>a>>b>>k;

      //If A and B are ints, then the sum of the digits can't be greater than 82
        if(k>82)
        {
        cout<<"0\n";
        }

        string s=tostring(a-1);
        string s2=tostring(b);

        memset(dp,-1,sizeof(dp));
        long long a1=dp_solve(s,0,1,0); //Solving for a-1


        memset(dp,-1,sizeof(dp));
        long long a2=dp_solve(s2, 0, 1, 0); //Solving for b

        cout<<a2-a1<<endl;


    return 0;
}
```


