
 

 

 

 

 

([C++](Cpp.md)) [HelloBoostXpressiveQtCreatorLubuntuToWindows](CppHelloBoostXpressiveQtCreatorLubuntuToWindows.md)
====================================================================================================================

 

![Boost](PicBoost.png)![Qt
Creator](PicQtCreator.png)![Lubuntu](PicLubuntu.png)![To](PicTo.png)![Windows](PicWindows.png)

 

[Hello Boost.Xpressive using Qt Creator under Lubuntu, crosscompiled to
Windows](CppHelloBoostXpressiveQtCreatorLubuntuToWindows.md) is a
[Hello Boost.Xpressive](CppHelloBoostXpressive.md) program.

 

-   [Download the Qt Creator project
    'CppHelloBoostXpressiveQtCreatorLubuntuToWindows' (zip)](CppHelloBoostXpressiveQtCreatorLubuntuToWindows.zip)

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

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppHelloBoostXpressiveQtCreatorLubuntuToWindows/CppHelloBoostXpressiveQtCreatorLubuntuToWindows.pro
----------------------------------------------------------------------------------------------------------------------------------------------

 

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` include(../../ConsoleApplication.pri) #Or use the code below # QT += core # QT += gui # greaterThan(QT_MAJOR_VERSION, 4): QT += widgets # CONFIG   += console # CONFIG   -= app_bundle # TEMPLATE = app # CONFIG(release, debug|release) { #   DEFINES += NDEBUG NTRACE_BILDERBIKKEL # } # QMAKE_CXXFLAGS += -std=c++11 -Wall -Wextra -Weffc++ # unix { #   QMAKE_CXXFLAGS += -Werror # }  include(../../Libraries/Boost.pri) #Or use the code below # win32 { #   INCLUDEPATH += \ #     ../../Libraries/boost_1_54_0 # }  SOURCES += main.cpp`
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostXpressiveQtCreatorLubuntuToWindows/main.cpp
----------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream>  #pragma GCC diagnostic push #pragma GCC diagnostic ignored "-Weffc++" #pragma GCC diagnostic ignored "-Wunused-local-typedefs" #include <boost/xpressive/xpressive.hpp> #pragma GCC diagnostic pop  ///Example adapted from http://www.boost.org/doc/libs/1_54_0/doc/html/xpressive/user_s_guide.html int main() {   const std::string hello( "hello world!" );    const boost::xpressive::sregex rex = boost::xpressive::sregex::compile( "(\\w+) (\\w+)!" );   boost::xpressive::smatch what;    if( boost::xpressive::regex_match( hello, what, rex ) )   {     std::cout << what[0] << '\n'; // whole match     std::cout << what[1] << '\n'; // first capture     std::cout << what[2] << '\n'; // second capture   } }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppHelloBoostXpressiveQtCreatorLubuntuToWindows/CppHelloBoostXpressiveQtCreatorLubuntuToWindows.sh
----------------------------------------------------------------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #!/bin/bash myfile="i686-pc-mingw32-qmake" mytarget="CppHelloBoostXpressiveQtCreatorLubuntuToWindows" myprofile=$mytarget.pro myexefile=release/$mytarget.exe   if [ -e $myfile ] then   echo "MXE crosscompiler '$myfile' found" else   echo "MXE crosscompiler '$myfile' not found directly, but perhaps it is in the PATH"   #exit fi  if [ -e $myprofile ] then   echo "Qt Creator project '$myprofile' found" else   echo "Qt Creator project '$myprofile' not found"   exit fi  echo "1/2: Creating Windows makefile"  $myfile $myprofile  if [ -e Makefile ] then   echo "Makefile created successfully" else   echo "FAIL: $myfile $myprofile"   exit fi  echo "2/2: Making makefile"  make  if [ -e $myexefile ] then   echo "SUCCESS" else   echo $myexefile   echo "FAIL" fi  #Cleaning up rm -r release rm -r debug rm Makefile rm Makefile.*`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

