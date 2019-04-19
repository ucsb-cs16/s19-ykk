---
num: "lect05"
lecture_date: 2019-04-16
desc: User Input; Functions
ready: true
reading: Section 4.3-4.6
---

# User Input

## Example of using command line arguments

* We can pass information into a C++ program through the command line when executing the program.
* Note: You may have to convert command line argument information into the proper type (i.e. convert it to an integer type) if necessary.
* The main function will need to have the following:

```
int main(int argc, char *argv[]) {
```

* `int argc` is the number of "arguments" the program has, including the executable name.
* `char* argv[]` is the "list" of arguments passed into the program.
	* Arguments are taken in as arrays of characters, known as "C-strings".
	* Don't worry if the syntax doesn't make too much sense for now, we'll cover this later in the quarter.
	* Use the square brackets [] to access specific indices of `argc`, where the arguments are stored.
	* The first argument, `argv[0]`, is the executable name

```c++
// cline.cpp
#include <iostream>
#include <cstdlib>

using namespace std;

int main(int argc, char *argv[]) {

	cout << "Number of arguments: " << argc << endl;

	cout << argv[0] << endl;
	cout << argv[1] << endl;
	cout << argv[2] << endl;

	// how to use these arguments as numbers?
	// We can convert them using the atoi function
	// in the cstdlib standard library

	int x = atoi(argv[1]) + atoi(argv[2]);
	cout << x << endl;
	return 0;
}
```

As you can see, the program expects three input arguments to the program:
```
    ./cline 1 2 3
```

If you don't provide the correct number of arguments, you will get a segmentation fault, since the computer will be accessing the uninitialized parts of the memory.
It is always best to check that the provided number of arguments matches what the program expects.
Here's the updated version of the above code:

```c++
#include <iostream>
#include <cstdlib>

using namespace std;

int main(int argc, char *argv[]) {
    int num_args = 4;

	cout << "Number of arguments: " << argc << endl;
	if (argc == num_args)
	{
		cout << argv[0] << endl;
		cout << argv[1] << endl;
		cout << argv[2] << endl;
		// how to use these arguments as numbers?
		// We can convert them using the atoi function
		// in the cstdlib standard library

		int x = atoi(argv[1]) + atoi(argv[2]);
		cout << x << endl;
	}
	else
	{
		//cout << "You need to provide 3 arguments after the name of the program.\n";
        // Subtract one to eliminate the first argument, which is the name of the program
		cout << "You need to provide " << (num_args - 1) << " arguments after the name of the program.\n";
	}
	return 0;
}
```

# Functions

* A function is a block of code that takes parameters, executes some statements, and sometimes returns a value.

* When developing software, defining functions is a way to "modularize" your code into maintainable parts.
	* Supports the DRY (Don’t Repeat Yourself) principle.
	* Better maintenance
		* If a bug exists in a function, change it once and it should fix it for everything that uses it.
	* General rule of thumb: if you find yourself writing the same code in different parts of the program, see if you can refactor that code into a function.


## Function Declarations

In C++, a function declaration must occur BEFORE they are used.
	* We can write the method after it is used, we just need to declare it.
	* Declaration must include: [return type] [function name] (input parameters)
	* Basically just the header of the function (its "signature"), followed by a semicolon
    * It is possible to leave out a function declaration, if you can place the entire function definition (the body) before the `main()`, but this is not common because it is often impractical to bury the `main()` function at the end of a file.

## Example: Simple Function Definition

```
#include <iostream>

using namespace std;

int areaOfSquare(int length); // declaration

int main() {
	int result = areaOfSquare(20); // call
	cout << result << endl;
	return 0;
}

int areaOfSquare(int length) { // definition
	return length * length;
}
// OK. Function declaration happens before it was used

-----------
#include <iostream>

using namespace std;

int main() {
	int result = areaOfSquare(20); // call
	cout << result << endl;
	return 0;
}

int areaOfSquare(int length) { // definition
	return length * length;
}
// ERROR! use of undeclared identifier 'areaOfSquare'

```

## Return vs. Print

* Not all functions need to return a value. Some cases may be
	* Printing something to a console
	* Simply changing a state of a variable or data structure.
	* Functions that don't return anything should have a return type `void`
* If you just want to print a value, and not save it, then it's more efficient to print it from a void function, rather than to return a value, save it in a variable, and then print it
* Can you have more than one `return` statement in a function?
  * Yes, but you can only return one value- once a `return` is executed, any other code below that line in the function is ignored. The program returns to the place where the funtion was initially called, with the returned value.

## Example of printing, but not returning

```
void printAreaOfSquare(int area) {
	cout << “Area of Square: “ << area << endl;
	return; // return not necessary, will exit function when reached.
}
```


# Memory Stack

* Types are important in compiled languages like C++
	* Knowing exactly the amount of memory a function will occupy is essential for memory organization during execution.
	* Function calls are laid out in memory as a data structure called a <b>stack</b>.
		* Think of a stack like a canister of tennis balls.
		* You can only add to the top of the stack.
		* You can only remove an item at the top of the stack.
	* Every time a function is called, memory footprint is created and added to the top of the memory stack.
		* That function must complete execution before it can be taken off the stack, and the process that originally called it can proceed.
	* When the function returns a value, the memory that was reserved for the function is removed from the stack.
	* `int main()` is the bottom most function on the stack throughout execution.

## Example

```
#include <iostream>

using namespace std;

int doubleValue(int x) {
	return 2 * x;
}

int quadrupleValue(int x) {
	return doubleValue(x) + doubleValue(x);
}

int main() {
	int result = quadrupleValue(4);
	cout << result << endl;
	return 0;
}
```

* Start Execution

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue(4)` is called

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(x)` is called

```
|                       |
|-----------------------|
| int doubleValue(4)         |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` is called again

```
|                       |
|-----------------------|
| int doubleValue(4)         |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue` returns the sum of the two `doubleValue(4)` function calls

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `main` prints the result of `quadrupleValue` return value. Program exits.



### Code written during lecture

The example shows how to do function overloading. Not included is the example of a function with the same input parameters but different return types, which results in an error.

```cpp
// print_hello.cpp
#include <iostream>
#include <cstdlib>
using namespace std;

double return_sum(double var, double x)
{
       return (var+x);
}

void print_hello(int var, int x)
{
    for (int i = 0; i < var; i = i+x)
    {
        cout << "Hello" << endl;
        cout << "var = " << var << " x = " << x << endl;
    }
    return;
}


void print_hello(int var)
{
    for (int i = 0; i < var; i++)
    {
        cout << "Hello" << endl;
    }
    return;
}

void print_hello()
{
    cout << "Hello" << endl;
    return;
}

int main(int argc, char* argv[])
{
    int user_count = -1;

    if (argc == 1)
    {
        cout<< "The name of your program is " << argv[0] << endl;
        return 0;
    }
    if (argc == 2)
    {
        user_count = atoi(argv[1]);
    }
    else {
        cout << "You didn't give us correct input!" << endl;
        exit(-1);
    }


    print_hello(user_count);

    cout << "___" << endl;
    print_hello(5, 2);

    cout << "___" << endl;
    cout << return_sum(15.5, 12.8) << endl;

    return 0;
}
```
