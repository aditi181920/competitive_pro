**Static non-member variables:**
--

-> Scope throughtout the program\
-> Retains value between function calls

**Static member variables:**
--

-> No association with any object\
-> Exist even when no object is defined\
-> They are declared (*static type var*) within the class but definied outside the class by *classname::var_name=val*\
```cpp
class X
{
public:
      static int i;
};
int X::i = 0; // definition outside class declaration assigning value here is optional
```
-> But only 1 definition allowed\
-> By default assigned 0 (if no value assigned)\
-> Static data members and their initializers can access other static pvt and protected members of the class
```cpp
class C {
      static int i;
      static int j;
      static int k;
      static int l;
      static int m;
      static int n;
      static int p;
      static int q;
      static int r;
      static int s;
      static int f() { return 0; }
      int a;
public:
      C() { a = 0; }
      };
      
C c;
int C::i = C::f();    // initialize with static member function
int C::j = C::i;      // initialize with another static data member
int C::k = c.f();     // initialize with member function from an object
int C::l = c.j;       // initialize with data member from an object
int C::s = c.a;       // initialize with nonstatic data member
int C::r = 1;         // initialize with a constant value


class Y : private C {} y;

int C::m = Y::f();    // error
int C::n = Y::r;      // error
int C::p = y.r;       // error
int C::q = y.f();     // error
Note: these cause error because the values used to initialize are pvt members of class Y which cannot be accessed

```
-> Can be made inline ,const(note that this can be defined inside class itself (*inline static int n=1;*)(*const static int n=1;*)),volatile but not mutable\
-> Note that constant initializer is not a definition, we still need to define it in the namespace scope
```cpp
#include <iostream>
using namespace std;

struct X {
  static const int a = 76;
};

const int X::a;

int main() {
  cout << X::a << endl;
}
```
-> If static data member is declared constexpr, it must be initialized with an initializer in which every expression is a constant expression, right inside the class definition.

**Static functions:**
--
-> Can only access other static variables or static functions present in the same class or data and function outside the class\
-> Called using class names
