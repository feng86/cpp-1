
 

 

 

 

 

([C++](Cpp.md)) [Assertion failed: !"Bad error code", file VMem.c, line 715](CppMiscErrorAssertionFailedBadErrorCodeVmemC.md)
===============================================================================================================================

 

[Misc error](CppMiscError.md).

 

 

 

 

 

Full error message
------------------

 

  ---------------------------------------------------------------
  ` Assertion failed: !"Bad error code", file VMem.c, line 715`
  ---------------------------------------------------------------

 

-   [View a screenshot of this error
    message](CppMiscErrorAssertionFailedBadErrorCodeVmemC.PNG)

 

 

 

 

 

Cause
-----

 

IDE: [C++ Builder](CppBuilder.md) 6.0

Project type: [VCL](CppVcl.md)

 

Appears when linking the following code:

 

  -------------------------------------------------------------------------
  ` #define ARRAY_SIZE 10000000  int main() {   int array[ARRAY_SIZE]; }`
  -------------------------------------------------------------------------

 

 

 

 

 

Solutions
---------

 

When this error occurs, restart [C++ Builder](CppBuilder.md) and
nothing has been lost. Do change the code as in one of the examples
below.

 

 

 

 

 

### Decrease the value of the [array](CppArray.md) size

 

  ------------------------------------------------------------------------
  ` #define ARRAY_SIZE 1000000  int main() {   int array[ARRAY_SIZE]; }`
  ------------------------------------------------------------------------

 

 

 

 

 

### Create the [array](CppArray.md) dynamically

 

  -------------------------------------------------------------------------------------------
  ` #define ARRAY_SIZE 10000000  int main() {   int * const array = new int(ARRAY_SIZE); }`
  -------------------------------------------------------------------------------------------

 

 

 

 

 

### Use a [std::vector](CppStdVector.md) (preferred)

 

  -------------------------------------------------------------------------------------------
  ` #include <vector>  int main() {   const int sz = 10000000;   std::vector<int> v(sz); }`
  -------------------------------------------------------------------------------------------

 

 

 

 

 

 

