
 

 

 

 

 

([C++](Cpp.md)) [std::underflow\_error](CppUnderflow_error.md)
================================================================

 

[std::underflow\_error](CppUnderflow_error.md) (a [derived
class](CppDerivedClass.md) from
[std::runtime\_error](CppRuntime_error.md)) is [thrown](CppThrow.md)
if a 'mathematical underflow occurs'. I did not yet succeed in producing
such a mathematical underflow.

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <stack> #include <stdexcept>  int main() {   std::stack<int> s;    try   {     //Too bad, pop does not throw std::underflow_error :-(     s.pop();   }   catch (std::underflow_error& e)   {     //Too bad, will not get here :-(     std::cout << e.what();   } }  `
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

