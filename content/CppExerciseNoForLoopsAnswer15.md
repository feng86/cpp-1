
 

 

 

 

 

([C++](Cpp.md)) [Answer of exercise \#9: No for-loops \#15](CppExerciseNoForLoopsAnswer15.md)
===============================================================================================

 

This is the answer of [Exercise \#9: No
for-loops](CppExerciseNoForLoops.md).

 

 

 

 

 

Question \#15: write to [std::cout](CppStdCout.md)
------------------------------------------------

 

Replace the [for](CppFor.md)-loop. You will need:

 

-   [std::copy](CppStdCopy.md)
-   [std::ostream\_iterator](CppStdOstream_iterator.md)

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <vector>   void CoutVector(std::vector<int>& v) {   const int sz = static_cast<int>(v.size());   for (int i=0; i!=sz; ++i)   {     std::cout << v[i] << '\n';   } }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Answer
------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <iterator> #include <ostream> #include <vector>   //From http://www.richelbilderbeek.nl/CppCoutVector.htm template <class T> void CoutVector(const std::vector<T>& v) {   std::copy(v.begin(),v.end(),std::ostream_iterator<T>(std::cout,"\n")); }`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

