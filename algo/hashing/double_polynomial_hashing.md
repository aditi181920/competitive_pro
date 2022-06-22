**DOUBLE POLYNOMIAL HASH:**
--

Since size of modulo m is limited, we can actually increase this by cheating a bit using the CHINESE REMAINDER THEOREM\
We can use 2 modulos here (simiarly u can also use 3 or more)\
take 1 hash value as 2^31-1 and other as 2^64 \
Note that we cant take first modulo as 2^64 since there are some anti hash test to figure this out\
And to take a good modulo difference between both modulos must fit in 2^32 bit integer \
For checking equality of strings now we can just checking equality of 2 hashes now instead of 1 single hash
