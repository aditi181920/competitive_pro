-> std::tuple is a generalization of std::pair (2 -> n)
-> ** declaration:** tuple<int, long long, char> b; (say)/
-> ** accessing data members: ** 
          
            -> get<0>(b), get<1>(b), get<2>(b), etc. (n in get<n>(b) should be known in compile time)
            -> using structure binding declarations:
                 auto [u, v, w] = b; 
               Then you can access the elements by using the variables
    
-> Comparison (<, <=, ==, ...) works with lexicographical order if all types are comparable
