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
-> if cur xor!=0 then next can always be made 0\


**SOME INTUTIONS AND INSIGHTS ON THE GAME OF NIM (FROM SOME CF BLOG):**
--

-> Since we can take stones fromn only 1 pile at a time, so it looks like a nice idea to get info from every pile and decompose that info to describe the game as a whole.\
-> For each game g, let us assign to it some integer "Nim-value" G which tells us whether this is a winning state or a losing state\
-> Let for 2 piles having a and b stones and having A and B nim values\
-> Then we define A^B to be Nim value of the game state a+b.\
-> Lets consider a simple game of p stones\
-> Then let's say the nim value for this is p\
-> Single pile is in winning state if p>0 and losing state if p=0. This is something we would like to see reflected in the Nim-values as well--- a Nim value G corresponds to  winning game state when G>0, and corresponds to a losing state when G=0\
-> Lets find way to composes these Nim values together with operator xor\
-> Associative: order of combining piles should not matter\
-> Identity: (A^0=A) If we place an empty pile it does not matter\
-> Inverse: (A^A=0) Whatever first person does.. other person will just mirror the moves in the other pile (since elements equal so he can always do this thing) \
-> We can see that all properties get along and especially the last property\
-> The inverse of every element is itself=> every non-zero element in grp has order 2. The only family of grps that have this property is the grp with set{0,1} and operation of addition modulo 2\
->Lets prove this xor rule of game of nim\
-> empty game is a losing state with Nim-sum 0.\
-> If current Nim sum is 0, then any move with make it non-zero (since we remove some non zero stones)\
-> If the current nim sum is non-zero, then there exists a move to make it equal to 0\
-> Say we removed s from pi stone pile .. then current xor becomes pi^(pi-s).\
-> Now let;s say current nim sum is N. then we need to remove some s from pi such that pi^(pi-s)=N\
-> This can be achieved always because \
-> since N is xor of all current piles there does exist some pile such tht msb of N is present in that pi\
-> Therefore we want such a pi and to make xor N (pi-s) should not have it \
-> We construct pi-s in such a way that we can obtain the required result\
-> All bit greater than msb of N keep it same as pi\
-> Off msb of N \
-> then rest it must match N^pi\
-> This construction is always less since msb is always different in both\
-> From here we can always recover s (since we know pi)\
-> This proves we can always do such a move\
-> If current player is in zero then next will always be in non-zero and he will always try to make next zero to make it lose\
-> Therefore if player have complete knowledge of the game state then the first player is helpless is Nim sum is 0 similarlty if non zero then he will always win\

**Extension on Nim and Grundy numbers:**
--

-> Usually game of nim problems are given through some variations\
-> Say instead of removing we can also add some stones\
---> this does not change anything since the amount of stones we add the other player can just remove the same stones bringing back to same state and since the game is finite therefore this adding is redundant in game of nim\
-> What if u can only take some square number of pile?\
-> Consider only single pile having p stones\
-> Let's reframe this as a directed graph\
-> Let p+1 vertices be there in graph(from 0 to p), each vertex corresponds to some game state\
-> Draw a directed edge from u to v if it is possible to transition from u stones to v with a valid move.\
-> We can imagine solving this with dp then using the terminal vertices as losing and using normal games rules on a DAG (all adj winning states-> then current is losing, atleast  1 losing state then current is winning state)\
-> Now let's try to see this using Nim-values, instead of assigning a win or loss, assign some integer value to each vertex such that 0 is a loss and nonzero is a win (Grundy numbers\Nimbers)\
-> Let G(u) of terminal =0\
-> Otherwise mex of everything else it points to\
-> We can see that this works since G(u) will be zero when no adj vertex has G(v) =0 implies no adj losing state => this is a losing state since this a winning state itself\
-> Now what about we have mulitple piles ? \
-> Spargue Grundy theorem says that these games are quivalent to playing Nim, but instead of getting Nim-sum by taking the xor of the piles, we take xor of their Grundy numbers\
-> In our normal game of Nim, each state points to every state smaller than it. Therefore G(p)=p which is consistent with our results about the original Nim\
-> mex is like a promise=> if G(p)=g then every 0-g-1 is in the list of valid moves from p\
-> Imagine transforming every pile in our game was transformed from having p stones but with weird rules, to G(p)=g stones but with normal Nim rules\
-> In nim we can transform from p stones to pile with size less than p
