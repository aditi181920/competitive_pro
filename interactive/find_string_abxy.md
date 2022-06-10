**FIND STRING THROUGH QUERYING:**
--

-> First character never repeats\
-> Query returns longest substring that appears in our query string that is prefix of real string\

Idea:
--

-> We can find 1st character in max 2 queries easily (group 2 )\
-> Now for rest cool trick is:\
-> We can find every next ith in 1 query only. How?\
-> pre->the ans string we have found till now\
-> query string-> pre+(no 1st character) + pre+(2nd character) + pre+(3rd charcater)+(1st charcter)+ pre(3rd)+(2nd) + pre(3rd)+(3rd)\
-> so if 1st type checker will return 0 else checker will return 1 else 2\
-> only for the last character again we need 2 queries
