**ABSTRACT CLASS:**
--

-> Abstract class- Contains atleast 1 pure virtual function\
-> used for using it as a base class\
-> cannot use it as a parameter, return type or even making the objects\
-> U can declare pointers and references though\
-> It can be derived \
-> A derived class unless all the pure virtual classes are overrided will be an abstract class as well\
-> An abstract class can be derived from a non abstract class \
-> An abstract class does not have anything else in its body


**VIRTUAL CLASSES:**
--

-> Virtual classes are primarily used during multiple inheritance. \
-> To avoid, multiple instances of the same class being taken to the same class which later causes ambiguity, virtual classes are used.\
```cpp
#include <iostream>
using namespace std;

class A {
  public:
    void display() {
      cout << "Hello form Class A \n";
    }
};

class B: public A {
};

class C: public A {
};

class D: public B, public C {
};

int main() {
  D object;
  object.display();
}

error: non-static member 'display' found in multiple base-class subobjects of type 'A':
    class D -> class B -> class A
    class D -> class C -> class A
    object.display();
           ^
note: member found by ambiguous name lookup
    void display()
         ^
1 error generated.
  
```

-> defining virtual class
```cpp
class B: virtual public A {
  /statement 1
};
class C: public virtual A {
  /statement 2
};
```

**Pure virtual function:**
--

-> A pure virtual function is a function that does nothing which means that you can declare a pure virtual function in the base class that does not have a description in the base class.\
-> But it is necessary to override these functions in derived classes otherwise they become abstract 
