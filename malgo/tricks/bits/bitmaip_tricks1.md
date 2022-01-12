1. **(x-1):**\
-> all bits including rightmost 1 and bits to right of it flipped 

2. **(x+1):**\
-> all trailing set bits flipped and first rightmost unset bit set

3. **(-x):**\
-> rightmost set bit as it is and all bits to the left of it flipped

4. **(x&(-x)):**\
-> gives rightmost set bit

5. **x^(x&(x-1)):**\
-> also gives rightmost set bit

6. **x|(1<<n):**\
-> returns x with nth bit set
