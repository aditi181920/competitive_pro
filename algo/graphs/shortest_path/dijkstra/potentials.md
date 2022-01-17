**USING POTENTIALS TO DEAL WITH NEGATIVE EDGES IN DIJKSTRA:**
--

-> Note though potentials provide a way to deal with graphs having negative weight edges using dijkstra but they don;t work when negative weight cycles are involved.\
-> Also we can't arebitrarily apply potentials to edges\

-> **1. How to provide potentials:**
---

-> Pick a vertex v, increase the weights of the incoming edges to v by some real value x and decrease the weights of outgoing edges from v by the same amount x\
```sh         
            -> C              
        2 /    ^
         /     |-10     ------------- 
        /      |                     |                       p(C)=-10, p(A)=0, p(B)=0
      A -----> B                     |
          5                          |
                                     \/
                                     
                                        -> C
                                    12/    ^
                                     /     |0
                                    /      |
                                   A -----> B
                                       5
```

**Def:** A function p:V->R is called a potential of graph G if for every edge (u->v) belonging E, it holds that w(u->v)+p(u)-p(v)>=0 [since p(u) is added to w(u->v) through node u and p(v) is subtracted from w(u->v) through node v; so effective offset of w(u->v) becomes p(u)-p(v) and this value should be >=0 because potentials are applied for removing negative weights]

![image](https://user-images.githubusercontent.com/94597499/149729266-1f518fa4-0582-400b-a052-71675f179d1c.png)
![image](https://user-images.githubusercontent.com/94597499/149729421-6eeb01a7-be03-44ff-a63a-e037c615319d.png)
![image](https://user-images.githubusercontent.com/94597499/149729488-9059f461-010e-43ba-8530-df05c4b36ffa.png)
![image](https://user-images.githubusercontent.com/94597499/149729626-6eb93866-d814-494f-bd52-4da2c4fa3c07.png)
