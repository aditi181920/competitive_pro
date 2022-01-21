**MAX XOR PAIR USING TRIE:**
--

-> **Insertion:**\
--> We can construct a path using bits from msb to lsb of every number\
--> note: for this implementation keep the number of bits for each number same before insertion by adding leading zeros if required 

--> Complexity: O(log2(maxn))

-> **Query:**\
--> for each number x we will find a number y by querying the trie such that xor is maximum.\
--> let's say x is b1,b2,b3,... where bi is corresponding bits. \
--> for XOR to be maximum we need to take dissimilar bits so if bi is 1 we need to go with a 0 and vice-versa if we can, if can't then go with what you can 


![image](https://user-images.githubusercontent.com/94597499/150489701-3ba2dbd2-de00-4070-b238-c47680ec511f.png)

![image](https://user-images.githubusercontent.com/94597499/150489718-9463c0d3-db54-4c25-9a3b-d4f4eea72c87.png)


--> Complexity: O(log2(maxn)*n)

**IMPLEMENTATION:**
```cpp
#define ll long long int
ll triee[1000000][2];
class Solution {
public:
    int tot;
    Solution(){
        tot=2;
        memset(triee,0,sizeof(triee));
    }
    void insert(ll x){
        ll node=1;
        for(int i=30;i>=0;i--){
            int bit=(1<<i)&x;
            if(bit>0)bit=1;
            if(triee[node][bit]==0){
                triee[node][bit]=tot;
                tot++;
            }
           // cout<<"node:"<<node<<" bit:"<<bit<<" triee[node][bit]:"<<triee[node][bit]<<"\n";
            node=triee[node][bit];
        }
    }
    ll query(ll x){
        ll node=1;
        ll ans=0;
        for(int i=30;i>=0;i--){
            int bit=(1<<i)&x;
            if(bit>0)bit=1;  // cout<<"node:"<<node<<" bit:"<<bit<<"\n";
            if(triee[node][!bit]==0){
                node=triee[node][bit];    // cout<<"no complemet| triee[node][bit]:"<<triee[node][bit]<<"\n";
                ans+=((1<<i)*bit);        // cout<<"ans:"<<ans<<"\n";
            }else{
                node=triee[node][!bit];   //cout<<"complemet| triee[node][bit]:"<<triee[node][bit]<<"\n";
                ans+=((1<<i)*(!bit));     //cout<<"ans:"<<ans<<"\n";
            }
        }
        return ans;
    }
    int findMaximumXOR(vector<int>& nums) {
        int n=nums.size();
        ll ans=0;
        for(int i=0;i<n;i++){ //cout<<"insert:\n";
            insert(nums[i]);  //cout<<"query:\n";
            ans=max(ans,query(nums[i])^nums[i]);
        }
        return ans;
        
    }
};
```
