# ([C++](Cpp.md)) [HelloBoostRegexQtCreatorUbuntu](CppHelloBoostRegexQtCreatorUbuntu.md)

## Technical facts

 * [Operating system(s) or programming environment(s)](CppOs.md)
    * ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)
 * [IDE(s)](CppIde.md):
    * ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1
 * [Project type](CppQtProjectType.md):
    * ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)
 * [C++ standard](CppStandard.md):
    * ![C++98](PicCpp98.png) [C++98](Cpp98.md)
 * [Compiler(s)](CppCompiler.md):
    * [G++](CppGpp.md) 4.9.2
 * [Libraries](CppLibrary.md) used:
    * ![Boost](PicBoost.png) [Boost](CppBoost.md): version 1.55
    * ![Qt](PicQt.png) [Qt](CppQt.md): version 5.4.1 (32 bit)
    * ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version 4.9.2

## [Qt project file](CppQtProjectFile.md): ./CppHelloBoostRegexQtCreatorUbuntu/CppHelloBoostRegexQtCreatorUbuntu.pro

```
QT       += core
QT       -= gui
CONFIG   += console
CONFIG   -= app_bundle
TEMPLATE = app
SOURCES += main.cpp

LIBS += \
  -lboost_date_time \
  -lboost_filesystem \
  -lboost_program_options \
  -lboost_regex \
  -lboost_signals \
  -lboost_system
```

## ./CppHelloBoostRegexQtCreatorUbuntu/main.cpp

```c++
#include <iostream>

#include <boost/regex.hpp>

int main()
{
  std::string s = "Hello World";
  s = boost::regex_replace(s,boost::regex("World"),std::string("Boost"));
  std::cout << s << '\n';
}
```

