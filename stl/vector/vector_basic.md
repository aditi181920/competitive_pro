-> header: <vector>\
-> a dynamic array\
-> behaves like stack : push to end and pop from end\
-> Comparison (<, <=, ==, ...) works with lexicographical order\
-> ** declaration: **
   
       vector<data_type> name(size,initial_val);  // 1-D vector..
                                                          // the things inside bracket is optional 
                                                      //if size not given then empty vector else n size vector contining n initial vals
                                                      //these 2 things also valid for 
       vector<vector<data_type>> name(rows,vector<data_type> (cols,initial_val);  // 2-D vector
                                                     // again bracket things are optional
                                               //but if you wish to define cols in 2nd bracket u must define all values in 1st 
  
-> ** some operations**
  ```sh
        1. random access : using []    O(1)
        2. Pushing an element :
                        -> insert_back()
                        -> emplace_back() :  faster than insert_back()
        3. Remove the last element : pop_back()
        4. clear : clear()
  
  ```
  
-> vector works on the idea of reallocation of :\
  --> if the array size is not large enough another array will be created usually with the doubled size and everything in the old array will be moved to new array\
  --> therefore a lot of moves may be involved for maintaining the dynamic nature of the vector
  
  
-> improving performance of vector:\
  --> Use reserve after declaration so the elements do not need to move many times\
  ------> Requests that the vector capacity be at least enough to contain n elements. If n is greater than the current capacity then reallocation will be done to satisfy the req\
  --> Use resize after declaration if you know the final size, then use it like an normal array\
  ------> resize ensures vector capacity is exactly what is being requested
                            
