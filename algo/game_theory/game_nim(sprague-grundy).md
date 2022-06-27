**GAME THEORY:**
--

**Properties req:**
--
1. **Impartial game:**\
-> Same set of moves is available for both players in every situation. Only difference is who mves first.

2. **Perfect infomation:**\
-> No info is hidden from anyone. Both know rules, possible moves.
  
3. **Finite game:**\
-> After certain moves one of the players end up in losing position (who can't move any further loses:Regular). No draws in this game.
                                                        
-> Such games can be described by DAG. Vertices-> game states, edges-> transitions(moves), no outgoing edge->losing vertex.\
-> losing vertex-> all moves leads to winning states, winning vertex-> atleast 1 transition to a losing state

**NIM:**
--
-> Any perfect information, impartial 2 player game can be reduced to the game of Nim. 


**Game description:**
--
-> Several piles, each with several stones. In a move, player can take any positive number of stones and remove. Player loses if he can't make any move

**Solution:**
--
-> The current player has a winning strategy iff the xor-sum(bitwise xor) of the pile sizes if non xero\
-> **PROOF BY INDUCTION:**\
-> When pile empty, xor-sum zero, theorem is true\
-> If the current position the xor- sum s=0. Consider any move, it will reduce size of a pile x to a size y.\
t=s xor x xor y = x xor y\
Since y<x, t can't be zero. => Any reachable state is a winning state, so we are in a losing position.\
-> If the current position the xor sum s!=0. Let d be msb in s. Move on a pile whose size's bit d is set (must exists since it exists in xor). Reduce size x to y = x xor s. y<x. t = s xor x xor y = s xor x xor ( s xor x) = 0\
=> we found a losing state and so the current state is a winning state

Corollary. Any state of Nim can be replaced by an equivalent state as long as the xor-sum doesn't change. Moreover, when analyzing a Nim with several piles, we can replace it with a single pile of size . ??


**EQUIVALENCE OF IMPARTIAL GAMES AND MIN (SPRAGUE - GRUNDY THEOREM)**
--
-> How to find a corresponding state of Nim, for any impartial game?\

**Lemma about Nim with increases:**
--
If we allow adding stones to a chosen pile. Exact rules abt how and when increasing is allowed is not important. However rules must keep our graph acyclic. \
**Lemma:** Addition of increasing to Nim does not change how losing and winning states are determined. They are useless\
**Proof:** If a player adds some thing, then other player can just undo his move by removing the same piles. Since acyclic graph, the player will run out of increasing moves without making any difference to the game and will have to do the usual Nim move. 

**Sprague-Grundy theorem:**
--
Consider a state v of a 2-player impartial game and let vi be the states reachable from it. We can assign a fully equivalent game of Nim with one pile size x (Grundy value or Nim value of state x). \
x=mex{x1,x2,...,xk}\
where xi is the grundy value for state vi\
Viewing the game as a graph, we can calc Grundy values starting from vertices without outgoing edges. Grundy value being equal to zero means a state is losing.

**PROOF BY INDUCTION:**
--
For vertices w/o a move, x=0(mex of empty set). Correct since Nim is losing.\
Consider any other vertex x, assuming the xi's correspondnig to its reachable vertices are already calculated.\
Let p=mex{x1,x2,...,xk}. For any integer i belongng to [0,p) there exists a reachable vertex with grundy value i. => state of game of Nim with increases with one pile of size p. In such a game we have transitions to piles of every size smaller than p and possibly transitions to piles with sizes greater than p. So, p is indeed desired grundy value for the currently considered state.

**ALGORITHM:**
--
-> Applicable to any impartial 2-player game.\
-> To calc Grundy value of a state u need to :\
1. Get all possible transitions from this state\
2. Each transition can lead to a sum of independent games. Calc Grundy for each independent game and xor them\
3. Find states's Grundy value by taking mex of these xor.\
4. If value is zero, then current state is losing, otherwise it is winning.

**Patterns in Grundy values:**
--
-> In some games there may exist some pattern in the grundy values, but in some cases it may not.
