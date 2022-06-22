**RABIN KARP:**
--

-> This algo is based on string hashing\
-> Problem: given pattern s, text t; does pattern s appears in text along with its occurences in O(|s|+|t|) time

**Algo:**
--

-> Calculate hash value for the pattern s\
-> Calculate prefixes of text t\
-> Compare each subtring of length |s| with the pattern.
