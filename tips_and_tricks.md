-> unorodered_map are hackable due to the fact that they are based on hash maps which does not perform very well in worst case because of large number of collisions.\
so map which are based on red-black trees are preferred\
-> order of cost : div>mul>abs>add,sub,compare  ..... div is 10 times add, mult 4 times add and pow being the costliest is 100 times the cost\
-> if u can make some data structures global then make it so in case u need a lot of memory and there are a lot of chance of stack overflow... but global space is vulnerable so be 
cautious as well
-> pass things by reference in functions for speed uo if u can\
-> div by const is well optimized by compilers\
-> computation of pre and post operators is done after encouter of semicolon. (so, value of a variable with pre post or none will be same until it encouters semicolon)\
-> vector takes more memory and time than array ... prefer array over vectors\
-> declare variables globally if can\
-> always pass by reference.. missing this out can actually cause a TLE when it should not\
