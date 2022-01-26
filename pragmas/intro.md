

-> pragmas are widely believed to make code faster, but sometimes may lead to slowdowns and even runtime errors on certain platform\
-> the pragmas differ by whether they are supported by gcc/c/c++ compilers so portability may vary from platform to platform (on cf though u can use them with less compiler restriction)\
-> #pragma directive is method specified by the C std for just providing some additional information to the compiler beyond what is conveyed in the language itself\
-> most GNU defined, supported pragmas have been given a GCC prefix. 

**PROBLEM OF #PRAGMA:**
--
-> #pragma being a directive, cannot be produced as the result of micro expansion\
-> _Pragma is an operator (introduced by C99) and much like sizeof or defined, and can be embedded in a macro\
-> syntax: _Pragma(*string-literal*) where string-literal can be either a normal or wide-character string literal.\
-> It is destringized, by replacing all '\\' with a single'\' and all '\' with a '"'. The result is then processed as if it had appeared as the right hand side of a '#pragma' directive'.\
-> Some equivalencies:
```sh
    #pragma GCC dependency "parse.y"

    _Pragma ("GCC dependency \"parse.y\"")

    #define DO_PRAGMA(x) _Pragma (#x)     note: # before variable returns name provided to variable
    DO_PRAGMA (GCC dependency "parse.y")
```
-> The standard is unclear on where a _Pragma operator can appear. The preprocessor does not accept it within a preprocessing conditional directive like ‘#if’. \
-> To be safe, you are probably best keeping it out of directives other than ‘#define’, and putting it on a line of its own.

--> Some pragmas meaningful to preprocessor\

1. #pragma GCC dependency:\
-> allows you to check the realtive dates of the current file and another file. If other file is more recent than the current file, a warning is issued.\
-> this is useful if the current file is derived from the other file, and should be regenerated.\
-> the other file is searched for using the normal include search path. Optional trailing text can be used to give more info in the warning msg
```sh
    #pragma GCC dependency "parse.y"
    #pragma GCC dependency "/usr/include/time.h" rerun fixincludes
```
2. #pragma GCC poison:\
-> helps to enforce some identifiers to stay outside of your program, if any of those identifiers appears anywhere in the source after the directive, error will be produced.\
-> Note that if identifier appears as part of expansion of macro which was defined before identifier was poisoned , it will not cause an error
```sh
    #pragma GCC poison printf sprintf fprintf
    sprintf(some_string, "hello");             ---> gives error
    
    #define strrchr rindex
    #pragma GCC poison rindex
    strrchr(some_string, 'h');                 ---> error free
```

3. #pragma GCC system_header:\
-> no argument\
-> causes rest of the code in the current file to be treated as if it came from a system header

4. #pragma GCC warning/#pragma GCC error:\
-> causes preprocessor to issue a warning diagnostic and error msg respectively with the text 'message'. \
-> the message contained in the pragma must be a single string literal\
-> unlike '#warning' and '#error' directives, these pragmas can be embedded in preprocessor macros using '_Pragma'

5. #pragma once:\
-> If #pragma once is seen when scanning a header file, that file will never be read again, no matter what.\
-> It is a less-portable alternative to using ‘#ifndef’ to guard the contents of header files against multiple inclusions.


