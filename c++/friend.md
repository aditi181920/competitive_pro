**FRIEND FUNCTIONS:**
--

-> These are functions or classes which have access to info of some other class which only the members of that class should have had (like pvt and protected data members)\
-> They aren;t member of class, they just have special priviledges\
-> Pvt (only class member accessible)\
-> Protected (class member+derived class accessible)\
-> Public(from anywhere)\

-> Functions with global scope can be declared as friend functions prior to their prototypes, member functions cannot be declared as friend functions before the appearance of their complete class declaration.
-> This rule is not applicable for friend classes completely though

```cpp
namespace NS
{
    class M
    {
        friend class F;  // Introduces F but doesn't define it
    };
}

namespace NS
{
    class M
    {
        friend F; // error C2433: 'NS::F': 'friend' not permitted on data declarations
    };
}

class F {};
namespace NS
{
    class M
    {
        friend F;  // OK
    };
}

template <typename T>
class my_class
{
    friend T;
    //...
};

class Foo {};
typedef Foo F;

class G
{
    friend F; // OK
    friend class F // Error C2371 -- redefinition
};
```

```cpp
// friend_functions.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class Point
{
    friend void ChangePrivate( Point & );
public:
    Point( void ) : m_i(0) {}
    void PrintPrivate( void ){cout << m_i << endl; }

private:
    int m_i;
};

void ChangePrivate ( Point &i ) { i.m_i++; }

int main()
{
   Point sPoint;
   sPoint.PrintPrivate();
   ChangePrivate(sPoint);
   sPoint.PrintPrivate();
// Output: 0
           1
}


// classes_as_friends1.cpp
// compile with: /c
class B;

class A {
public:
   int Func1( B& b );

private:
   int Func2( B& b );
};

class B {
private:
   int _b;

   // A::Func1 is a friend function to class B
   // so A::Func1 has access to all members of B
   friend int A::Func1( B& );
};

int A::Func1( B& b ) { return b._b; }   // OK
int A::Func2( B& b ) { return b._b; }   // C2248


// classes_as_friends2.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class YourClass {
friend class YourOtherClass;  // Declare a friend class
public:
   YourClass() : topSecret(0){}
   void printMember() { cout << topSecret << endl; }
private:
   int topSecret;
};

class YourOtherClass {
public:
   void change( YourClass& yc, int x ){yc.topSecret = x;}
};

int main() {
   YourClass yc1;
   YourOtherClass yoc1;
   yc1.printMember();
   yoc1.change( yc1, 5 );
   yc1.printMember();
}


```

-> Friends can be made inline 

