---
num: "lect08"
lecture_date: 2019-04-30
desc: "Intro to lab04: Arrays; C++ Build Process, Makefiles, TDD"
ready: true
reading: Lecture notes; Section 7.1 up to p.388
---



# Arrays

* An array is used to organize a collection of values of the same type.
* So far, we have been writing programs where values aren’t stored in a collection, but single variables.
* Another way to think of arrays under-the-hood is a sequence of cells that are stored <i>contiguously</i> in memory.


## Declaring Arrays

```
int arr[10];
```

* Arrays need a type defined (`int`), a variable name (`arr`) and a size (`10`).


## Bracket Syntax
* Accessing an individual cell of an array uses a traditional `[ ]` syntax, which is indexed starting at 0.
	* The first element is arr[0]. The last element is arr[9].
	* Initially, each cell is undefined (may contain junk data).
		* Remember, it's important to explicitly initialize values in C++.

```
int arr[100];
for (int i = 0; i < 100; i++) {
	cout << arr[i] << endl;
}
```

* Notice how some elements in the array may contain random values since we didn't initialize values in the array.

## Example of reading / writing values from / to the array

```
arr[0] = 1;
arr[1] = -5;
arr[1] = arr[0]; // fetching and storing array values
```

* For all practical purposes, an element in an array can be treated as a value whose type is what the array was defined as.
* An example using `cin`:

```
int arr[10];
cout << "Enter a number: ";
cin >> arr[0];
cout << "arr[0] = " << arr[0] << endl;
```

* An example using functions

```
void passArrayValueExample(int x) {
	cout << “Parameter value: “ << x << endl;
}

int main() {
	int x[1];
	x[0] = 3;
	passArrayValueExample(a[0]); // prints 3
}
```

## Example of iterating through the entire array

```
int arr[10];
for (int i = 0; i < 10; i++) {
	arr[i] = i; // initializes elements using i
}
int num = arr[5] + 2;
cout << num << endl; // 7
```

* Unlike some languages, C++ arrays cannot be indexed with negative numbers.
* Arrays do not know what their size is, so programmers will need to keep track of that.


-------------


# C++ Build Process

* So far we’ve been writing and compiling small programs in a single file.
* Though typical C++ programs may be organized into small pieces where functionality is defined in separate files.

## Header Files
* A header file is a file that typically contains only declarations.
* .cpp files contains “source code" for that functionality
* Typically, each source file contains a corresponding header file with definitions you want to have accessible to other source files.
* Source files that need to use any of the functions from other source files will need to include the header file.
	* By doing this, we are declaring functions in the file (remember we must declare or define functions before using them in our code).

## Example

```
------------------------------------
// drawShapes.h
#include <string>
using namespace std;

string drawRightTriangle(int height);
string drawSquare(int length);
------------------------------------
// drawShapes.cpp
#include <string>
using namespace std;

string drawRightTriangle(int height) {
	string result = "";
	int rowLength = 1;

	for (int i = 0; i < height; i++) {
		for (int j = 0; j < rowLength; j++) {
			result += "*";
		}
		result += "\n";
		rowLength++;
	}
	return result;
}

string drawSquare(int length) {
	string result = "";

	for (int i = 0; i < length; i++) {
		for (int j = 0; j < length; j++) {
			result += "*";
		}
		result += "\n";
	}
	return result;
}
------------------------------------
//program1.cpp
#include <iostream>
#include "drawShapes.h"

int main() {
	cout << drawRightTriangle(5) << endl;
	cout << drawSquare(5) << endl;	
return 0;
}
------------------------------------
```

## What’s with the different type of #include<> or #include ""?

* Having "'#include<>'" includes libraries from the C++ Standard Library
* For our own header files, we use `#include ""`
	* For example, when we use `#include<iostream>`, all the declarations in the I/O stream library including cout, cin, endl, etc. are available for use in our file.
	* When we use `#include "drawShapes.h"`, all of the declarations in the drawShapes.h file is included in the file.	
  * This allows us to call these functions in our file.

Similar to how we compile C++ programs with a single file, we can compile all source (.cpp) files using:

`g++ -o program1 program1.cpp drawShapes.cpp`

* This approach works, but can be inefficient when compiling MANY files.
	* Imagine making a small change in one file, then ALL files using this command will be recompiled.

* A more efficient way would be to compile each piece separately and link all pieces together at the end.
	* This way, if only one file changed, then only that one file needs to be re-compiled.
	* Compiling a file produces a lower-level form of the file (called an object file (.o)).
	* The Linker then takes these .o files and puts them together to form the actual executable.
	* We can accomplish this as follows:

```
g++ -c -o drawShapes.o drawShapes.cpp
g++ -c -o program1.o program1.cpp
g++ -o program1 program1.o drawShapes.o
```

* If we only make a change to program1.cpp, all we need to do is recompile the program1.o file.

## C++ Build Process

1.	Preprocessing: Text-based program that runs before the compilation step. Looks for statements such as `#include` and modifies the source which is the input for compilation.
	* Think of the compiler "copying / pasting" the contents of the included file everytime `#include` is used.

2.	Compilation: Translates source code into “object code,” which is a lower-level representation optimized for executing instructions on the specific platform. Lower level representations are usually stored in a .o (object) file.

3.	Linking: Resolves dependencies and maps appropriate functions located in various object files. The output of the linker is an executable file for the specific platform.

## But what happens if we have hundreds of source files to compile?
* Manually compiling everything can be really cumbersome and error-prone.
* Makefiles are a way to automate this process by defining compilation rules.

# Makefiles

## General Format of a Makefile

```
[target]: [dependencies]
	[commands]
```

[Check out more information on compilation / makefiles](https://foo.cs.ucsb.edu/16wiki/index.php/C%2B%2B:_Separate_Compilation_and_Makefiles).


## Example

```
------
# Makefile

# Single line comments in Makefiles use '#'

program1: program1.o drawShapes.o
	g++ -o program1 program1.o drawShapes.o

clean:
	/bin/rm -f *.o program1
------
```

* If a change to a .cpp file is made, then only that .cpp file gets recompiled.
* If no changes were made, make knows not to do anything.
	* Uses timestamps to determine if a .o file needs to be recompiled.

* `make program1` will check if program1.o and drawShapes.o is present.
	* `make` will try to generate the .o files if they aren't available.
	* Once .o files are generated, the command is executed, which generates the executable by linking the .o files together.
* `make clean` will remove all .o files and the executable `program1`

## Example

```
$ make program1
c++    -c -o program1.o program1.cpp
c++    -c -o drawShapes.o drawShapes.cpp
g++ -o program1 program1.o drawShapes.o
```

* If we make a small change to program1.cpp, save the file, and run the make command again:

```
$ make program1
c++    -c -o program1.o program1.cpp
g++ -o program1 program1.o drawShapes.o
```

* Only the program1.o file is recompiled.
* `make` knows the other .cpp files haven't been updated (using timestamps) so it doesn't need to recompile these .o files.
* If we try executing `make program1` again without any changes, then nothing happens since no updates to any .o files are needed.

```
$ make program1
make: `program1' is up to date.
```

# Another Example of a Test Program

## Test-Driven Development (TDD)
* Write test cases that describe what the intended behavior of a unit of software should BEFORE implementing the functionality.
	* Defines the requirements of your piece of software.
* Implement the details of the functionality with the intention of passing the tests.
	* Repeat until the tests pass.
* Imagine large software products where dozens of engineers are trying to add new features / implement optimizations all at the same time.
	* Having a “suite” of tests before deploying software to the public is essential.
	* Someone may modify changes that work for a current version, but breaks functionality in another version
	* Rigorous tests enable confidence in the stability in software.
* Gradescope system does something similar
	* It tests your submitted code and ensures functionality is correct by passing tests.

* We can define our testing functionality into `tdd.h` and `tdd.cpp`

```
------------------------------------
// tdd.h
#include <string>
using namespace std;

void assertEqual(string expected, string actual, string message="");
------------------------------------
// tdd.cpp
#include <iostream>
#include <string>
using namespace std;

void assertEqual(string expected, string actual, string message = "") {
	if (expected == actual) {
		cout << "PASSED: " << message << endl;
	} else {
		cout << "\tFAILED: " << message << endl;
		cout << "Expected: " << "[\n" << expected <<
		"\n]" << "Actual: [\n" << actual << "\n]" << endl;
	}
}
------------------------------------
//testDrawShapes.cpp
#include <iostream>
#include <string>
#include "drawShapes.h"
#include "tdd.h"
using namespace std;

void testDrawRightTriangle() {
	string expected1 =
	"*\n"
	"**\n";

	string actual1 = drawRightTriangle(2);
	assertEqual(expected1, actual1, " testHeight:2");

	string expected2 =
	"*\n"
	"**\n"
	"***\n";

	string actual2 = drawRightTriangle(3);
	assertEqual(expected2, actual2, " testHeight:3");
}

void testDrawSquare() {
	string expected1 =
	"**\n"
	"**\n";

	string actual1 = drawSquare(2);
	assertEqual(expected1, actual1, " testLength: 2");

	string expected2 =
	"***\n"
	"***\n"
	"***\n";

	string actual2 = drawSquare(3);
	assertEqual(expected2, actual2, " testLength: 3");
}

int main() {
	testDrawRightTriangle();
	testDrawSquare();
}
------------------------------------
# Makefile

testDrawShapes: testDrawShapes.o drawShapes.o tdd.o
	g++ testDrawShapes.o drawShapes.o tdd.o -o testDrawShapes

clean:
	/bin/rm -f *.o testDrawShapes
------------------------------------
```

* To use make to compile your code into an executable called `testDrawShapes`:

```
make testDrawShapes
```



# Code from Lecture

We first looked at how to declare an array and output the values of an uninitialized array (notice the junk values!).

```cpp
// main.cpp

#include <iostream>
using namespace std;

int main()
{
    const int SIZE = 20;
    int arr[SIZE];

    for (int i = 0; i < SIZE; i++)
    {
        cout << "[" << i << "] ";
        cout << arr[i] << endl;
    }

    cout << "Last element " << arr[SIZE] << endl;

    return 0;
}
```


We then asked the user to provide integer values that were stored in the array.

```cpp
#include <iostream>
using namespace std;

int main()
{
    const int SIZE = 3;
    int arr[SIZE];

    cout << "Enter " << SIZE << " numbers.\n";
    for (int i = 0; i < SIZE; i++)
    {
        cout << "[" << i << "] ";
        cin >> arr[i];
    } //end for

    cout << "Contents of the array\n";
    for (int i = 0; i < SIZE; i++)
    {
        cout << "[" << i << "] ";
        cout << arr[i] << endl;
    }

    return 0;
}
```


We tried to create a function to print the contents of the array. Interestingly, this code resulted in a compiler error (`print_Arr.cpp:21:16: error: use of undeclared identifier 'аrr'`), which apparently was caused by the accidental keyboard/language switch: the `a` that's in the `arr` variable is from the Cyrilic alphabet, which is outside the expected ASCII range. Mystery solved! The code should compile and run for you (unless you copy it from here without fixing it first ;-)).

```cpp
// print_Arr.cpp
#include <iostream>
using namespace std;

void print_arr(int array[], int arr_size);

int main()
{
    const int SIZE = 3;
    int arr[SIZE];

    cout << "Enter " << SIZE << " numbers.\n";
    for (int i = 0; i < SIZE; i++)
    {
        cout << "[" << i << "] ";
        cin >> arr[i];
    } //end for

    cout << "Increment the contents of the array\n";
    print_аrr(аrr, SIZE);
    for (int i =0; i < SIZE; i++)
    {
        //cout << arr[i] = arr[i] + 3 << endl;
        arr[i] = arr[i] + 3;
        cout << arr[i] << endl;
    }


    return 0;
}
void print_arr(int array[], int arr_size)
{
    for (int i = 0; i < arr_size; i++)
    {
        cout << "[" << i << "] ";
        cout << array[i] << endl;
    }
}
```


Lastly, we created a very simple setup using a header and a corresponding cpp file along with the main test program.

The declaration

```cpp
// print.h
#include <string>
using namespace std;

void print_smth(string text);
```

The definition

```cpp
print.cpp
#include <iostream> // notice that you don't need to include print.h here
using namespace std;

void print_smth(string text)
{
    cout << text << endl;
}
```

The test program

```cpp
// testprint.cpp

#include <iostream>
#include "print.h"

int main()
{
    print_smth("Hello!");
    return 0;
}
```

If we try to compile only the test program, we will get a **linker error**:
```
g++ testprint.cpp
Undefined symbols for architecture x86_64:
  "print_smth(std::__1::basic_string<char, std::__1::char_traits<char>, std::__1::allocator<char> >)", referenced from:
      _main in testprint-d213ed.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

In order to successfully compile it, we need to also compile the **source file** for the functions is print.h:

```
lec08 $ g++ testprint.cpp print.cpp
lec08 $ ./a.out
Hello!
```
