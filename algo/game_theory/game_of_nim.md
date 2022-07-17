**GAME OF NIM:**
--

-> Nim: players taking turns removing objects from distinct piles\
-> Nim sum: xor of all pile sizes\
-> If nim-sum is 0: current player will always lose\
-> Strategy to win is every player tries to reduce the nim-sum to 0 after his turn\
-> This is always possible if nim sum is not zero before his move\
-> How?\
-> x=x1^x2^x3^x4..\
-> 0=x^x1^x2^x3...\
-> pick some pile i such that x^xi <xi ... then we can reduce that pile \
-> why such pile always exists? if x has dth msb set then there must exist some xi which has the same msb set (following the property of xor)\
-> if there are only 2 piles left the player who starts alwyas wins cause then he can make 2 piles same then whatever the other player does player one copies so player two will lose in the end\
-> if current xor =0 then next xor!=0 no matter what we do\
-> if cur xor!=0 then next can always be made 0
