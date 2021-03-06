
 

 

 

 

 

([C++](Cpp.md)) [How to cross-compile a Qt Creator project from Ubuntu to a windows executable: example 9: any application, use of the moc variable](CppQtCrosscompileToWindowsExample9.md)
=============================================================================================================================================================================================

 

This is example 9, and perhaps a viable solutions of answering the [Qt
FAQ](CppQtFaq.md) [How to cross-compile a Qt Creator project from
Ubuntu to a windows executable?](CppQtCrosscompileToWindows.md), which
follows \[1\].

 

 

 

 

 

 

Downloads
---------

 

 

 

 

 

 

Project information

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.md): [Qt Creator](CppQtCreator.md) 2.0.0

[Project type](CppQtProjectType.md): [GUI](CppGui.md) application

[Compiler](CppCompiler.md): [G++](CppGpp.md) 4.4.1

[Libraries](CppLibrary.md) used:

-   [Boost](CppBoost.md): version 1.40
-   [STL](CppStl.md): from [GCC](CppGcc.md), shipped with [Qt
    Creator](CppQt.md) 2.0.0

 

 

 

 

 

[Qt project file](CppQtProjectFile.md)
---------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #------------------------------------------------- # # Project created by QtCreator 2010-09-25T09:43:28 # #------------------------------------------------- QT       += core QT       -= gui LIBS += -L/usr/local/lib -lboost_filesystem TARGET = CppQtCrosscompileToWindowsExample5 CONFIG   += console CONFIG   -= app_bundle TEMPLATE = app SOURCES += main.cpp`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

main.cpp
--------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` ///CppQtCrosscompilerToWindowsExample3: ///cross-compiling a console application with ///a library (that is: boost_filesystem). //--------------------------------------------------------------------------- #include <iostream> #include <string> #include <vector> //--------------------------------------------------------------------------- #include <boost/filesystem.hpp> //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetFilesInFolder.htm const std::vector<std::string> GetFilesInFolder(const std::string& folder) {   std::vector<std::string> v;    const boost::filesystem::path my_folder     = boost::filesystem::system_complete(         boost::filesystem::path(folder));    if (!boost::filesystem::is_directory(my_folder)) return v;    const boost::filesystem::directory_iterator j;   for ( boost::filesystem::directory_iterator i(my_folder);         i != j;         ++i)   {     if ( boost::filesystem::is_regular_file( i->status() ) )     {       const std::string filename = i->path().filename();       //const std::string full_filename = folder + "/" + filename;       v.push_back(filename);     }   }   return v; } //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetPath.htm const std::string GetPath(const std::string& filename) {   return boost::filesystem::path(filename).parent_path().string(); } //--------------------------------------------------------------------------- int main(int, char* argv[]) {   const std::vector<std::string> v = GetFilesInFolder(GetPath(argv[0]));   std::copy(v.begin(),v.end(),std::ostream_iterator<std::string>(std::cout,"\n"));   std::cout << "Number of files: " << v.size() << '\n'; } //---------------------------------------------------------------------------`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Process
-------

 

For this example, I use a console project that calls the Boost
libraries. If you only need the STL, [example 1: console application, no
libaries](CppQtCrosscompileToWindowsExample1.md) shows an easy and
successfull approach.

 

Additional qmake arguments can be supplied in the 'Projects -&gt; Build
Settings -&gt; Build Steps -&gt; qmake -&gt; Additional arguments' edit.

-   [Where to add qmake
    arguments (png)](CppQtCrosscompileToWindowsExample5.png)

 

NOTE: \[1\] IS ABOUT MAC!

 

 

 

 

 

[References](CppReferences.md)
-------------------------------

 * [1] [https://blog.qt.io/blog/2009/10/12/to-make-or-not-to-make-qmake-and-beyond/](https://blog.qt.io/blog/2009/10/12/to-make-or-not-to-make-qmake-and-beyond/)
 
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` 5) Cross-compiling  In large mixed cross-compiled (were you compile projects for both host and target systems at the same time) projects, most of the sub-projects normally compile for the target system, while only a few (supporting) projects are intended for the host. This means that projects should easily and automatically pick up the target platform, while a bit more attention should be required for host platform projects only.  The project shouldn?t have to worry too much about which platform, nor how to manipulate the project file to achieve the result. Ideally they would only have to mark that a project is intended for the host platform, like for example:      var moc = {         "target" : "moc",         "platform": "Host",         "defines" : { "all"           : ["QT_MOC"]},         ...         }  As the configure process has already figured out which parameters are needed for the host and target platform, the build system would know which defaults to apply to each project type in the cross-compiling setup; so the project developer need not do anything else to the project, unless he/she needs to override the cross-compiling defaults.`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

