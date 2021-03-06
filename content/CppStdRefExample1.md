
 

 

 

 

 

([C++](Cpp.md)) [StdRefExample1](CppStdRefExample1.md)
========================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++11](PicCpp11.png) [C++11](Cpp11.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStdRefExample1/CppStdRefExample1.pro
----------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Werror SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStdRefExample1/main.cpp
----------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <cassert> #include <functional>  int main() {   int a = 42;    //Reference-wrap a   const std::reference_wrapper<int> b(a);    //Const-reference-wrap the reference-wrap of a   const std::reference_wrapper<const int> c(b);    //Cannot do a non-const wrap around const-wrap c   //const boost::reference_wrapper<int> d(c); //Won't compile    assert(a == 42 && a == b && b == c);   ++a;   assert(a == 43 && a == b && b == c);   ++b;   assert(a == 44 && a == b && b == c);    //Cannot modify a const-wrap   //++c; //Won't compile }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

