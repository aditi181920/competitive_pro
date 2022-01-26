**LOGARITHM:**
---

**PROPERTIES OF LOG:**
--

1. log<sub>b</sub>(mn) = log<sub>b</sub>m+log<sub>b</sub>n    (product property)
2. log<sub>b</sub>(m/n) = log<sub>b</sub>m-log<sub>b</sub>n   (quotient property)
3. log<sub>b</sub>(m<sup>p</sup>) = p.log<sub>b</sub> (m)     (power property) 
4. log <sub>a</sub> x = log<sub>b</sub> x / log<sub>b</sub> a (change of base property)
5. log<sub>b</sub> b = 1          
6. log<sub>b</sub> 1 = log<sub>b</sub> (x<sup>0</sup>) = 0
7. b<sup> log<sub>b</sub>x</sup>=x

**FINDING NUMBER OF DIGITS USING LOG N :**
--

**FORMULA:**
d = floor(log<sub>b</sub> n) + 1

**PROOF:**

-> let's consider base 10\
-> 10<sup>d</sup> is the smallest number with d+1 digits\
-> 10<sup>d-1</sup> is the smallest number with d digits\
-> if n has d digits:  10<sup>d-1</sup><=n<10<sup>d</sup>\
-> taking log10 both sides \
-> d-1<= log<sub>10</sub>n <d\
-> therefore taking floor will give d-1 and add 1 to get d
