
 

 

 

 

 

([C++](Cpp.md)) [StdRatioExample1](CppStdRatioExample1.md)
============================================================

 

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

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppStdRatioExample1/CppStdRatioExample1.pro
--------------------------------------------------------------------------------------

 

  -------------------------------------------------------------------------------------------------------------------------------------------------------
  ` TEMPLATE = app CONFIG += console CONFIG -= app_bundle CONFIG -= qt QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ -Werror SOURCES += main.cpp`
  -------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppStdRatioExample1/main.cpp
------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <ratio>  int main() {   static_assert(std::ratio<7,-21>::num == -1,     "std::ratio simplifies, takes sign to numerator");   static_assert(std::ratio<7,-21>::den ==  3,     "std::ratio simplifies, takes sign to numerator");    static_assert(std::ratio_add<std::ratio<1,3>,std::ratio<1,6>>::num == 1,"1/3 + 1/6 == 1/2");   static_assert(std::ratio_add<std::ratio<1,3>,std::ratio<1,6>>::den == 2,"1/3 + 1/6 == 1/2"); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

