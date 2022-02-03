**EXTENTIONS:**
--
It generates some special assembly instruction or reduces some overhead leading to slightly faster programs\
Note that if your choice of algorithm and technique is not correct which leads the time limit to exceed sufficiently enough then these extensions may not help you in any ways\
However, in some cases if your program runs on slightly smalles cases on time or is just too little behind req. time then u may be able to squeeze out a little more performance

1. **INLINE FUNCTIONS:**
---
-> supported by GCC in both C and C++\
-> Inline function is one that is inserted in place at each call site, eliminating a function call overhead.\
-> But coping function definitions to place where it is called consumes extra instructions (thus memory bandwidth and instruction cache), so this is only worthwhile for very short functions (typically a line or two) which are called often.\
-> Inline functions are often recommended as a safer alternative to macros, since the usual function call semantics (such as type checkinig and single evaluation of the arguments) applies to inline functions. Since they are inserted in place, they are just as fast as macros.\
-> To make a non-member function inline just precede the function return type (in the very beginning of its definition) with the keyword inline\
-> To make a member function inline: Any member function whose body is defined in-place(i.e. inside the class) will be automatically inlined. If u prefer to keep the function body separate, apply the inline keyword to the declaration, but not to the definition.\
-> There is no guarantee that the function will be inlined; this is merely a request to the compiler.\
-> Recursive functions cannot be inlined\
-> GCC also refuses to inline funcion that use variable-sized arrays\
-> Any call through a function pointer will not be inlined; this means that trying to inline a comparison function to be passed to sort is futile.\
( If, however, you define a function object with an inlined operator() and pass an instance to sort, then the sort template will be specialised for that function class and the inlining will work.)

2. **COMPARISONS:**
---
-> **min** and **max** functions provided by <algorithm> has a limitation that they have only one template parameter, which specifies the type for both arguments; this often leads to errors when given arguments are of different types\
-> GCC provides the highly non-std operators <?(min) and >?(max), which will coerce the arguments to a suitable type. These operators are most commonly seen in their assignment forms <?= and >?=
```cpp
int m = INT_MAX;
for (int i = 0; i < N; i++)
    m <?= func(i);
```

3. **TYPEOF OPERATORS:**
---
-> One of the problems in defining macros is that the types involved are not always known\
-> the non-std typeof keyword can help here.\
-> It returns the type of the argument: a typeof expression can be used anywhere you'd normally write the name of a type, such as in declaration. 
```cpp
#define for_range(i, first, last) for (typeof(first) i = (first); i != (last); ++i)
```

4. **COMPOUND LITERALS:**
---
-> let's say we want to hold 2 or three items. we can definitely use pair or struct (or some other option maybe).\
-> one advantage u lose when u do this is the make_pair function creates pairs on the fly. You could of course define such a function for your class, or give it a constructor, but this can take vital coding time. GCC provides another alternative, which comes from C99: the compound literal. A compound literal is a mix between a cast and an initialiser. To understand what I mean, consider a struct defined as
```cpp
struct edge
{
    int target;
    int cost;
};
```
An example of a compound literal is (edge) { t, c } where t and c are expressions. The values in the braces are used to initialise the values of the struct, in the order in which they are declared. This is useful for instantiating structs on-the-fly to pass to STL methods.

5. **BIT MANIPULATION:**
---
Although C++ provides the bitset template to efficiently manipulate sets of bits, there are some things that can be done within an integral type that cannot be done so easily with a bitset. 
For example, the lowest bit of an integer x can be cleared by x &= x - 1. 
The x86 instruction set provides some special instructions for doing some types of bit manipulation, and GCC provides pseudo-functions that generate these instructions:
__builtin_ctz(unsigned int x)
Counts the number of trailing zero bits. This is one less than the POSIX function ffs (which GCC also implements using the special x86 instruction).
__builtin_clz(unsigned int x)
Counts the number of leading zero bits. Note that GCC docs state that both of these functions are undefined if x is 0. Experimenting on my Athlon 64 with GCC 3.4 gives values of 0 and 31 respectively with -O2, but nonsense values when compiled without optimisation. Don't rely on any particular value.
__builtin_popcount(unsigned int x)
Counts the total number of one bits in x. Note that x86 does not have an instruction to do this, so you end up calling a real function; however, this is still more convenient than having to write the function yourself.
These functions also have variants with ll appended to the function name, that takes unsigned long long rather than unsigned int.
