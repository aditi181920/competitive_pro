-> std:: pair is a struct template to store two objects\
-> To declare a pair: pair<int, long long> a;\
-> **accessing data member of pair:**
   
       -> simple access: a.first , a.second
       -> using structured binding declarations: 
       --> can assign data members of a to some variables x and y by :
       auto [x, y] = a;
       then we can just use x and y variables to access the members
       note: these type of declarations cannot be captured by lambda expressions
           like reference a structure binding is an alias to an existing object

-> Comparison (<, <=, ==, ...) works with lexicographical order if all types are comparable
