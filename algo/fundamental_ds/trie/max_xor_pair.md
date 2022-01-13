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

--> Complexity: O(log2(maxn)*n)
