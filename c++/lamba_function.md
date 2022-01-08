**DEF:**
--
-> anonymous function object (functor)\
-> we can define it locally where we want to call it or we can pass it as an argument to a function\

**GENERAL SYNTAX:**
--
``` sh
   (Capture clause) (parameter_list) mutable exception ->return_type
    {
         Method definition;
     }
```

**CAPTURE-CLAUSE:**
--
-> used to specify which variables are captured and whether they are captured by reference or by value.\
-> An empty capture closure [ ], indicates that no variables are used by lambda which means it can only access variables that are local to it.

```sh
   1. modes : 
      --> & : capture by ref
      --> = : capture by default
   2. If the capture clause contains capture-default =, then the capture clause cannot have the form = identifier.
       similarly holds for capture default &
   3. An identifier or ‘this’ cannot appear more than once in the capture clause.
```

```
[&sum, sum_var]             //OK, explicitly specified capture by value
[sum_var, &sum]           //ok, explicitly specified capture by reference
[&, &sum_var]              // error, & is the default still sum_var preceded by &
[i, i]                                //error, i is used more than once
```
**PARAMETER - LIST :**
--
-> optional\
-> similar to parameter list of method

**EXCEPTION:**
--
-> Exception specification\
-> Optional\
-> Use “noexcept” to indicate that lambda does not throw an exception.

**RETURN TYPE:** 
--
-> Optional\
-> The compiler deduces the return type of the expression on its own\
-> But as lambdas get more complex, it is better to include return type as the compiler may not be able to deduce the return type.

**METHOD DEFINITION:**
--
-> Lambda body.
