---
num: "lect07"
lecture_date: 2019-04-23
desc: "Midterm preparation and overview / Reading from files"
ready: true
reading: Sections 6.1 and 6.2
---

# Code from Lecture

Introducing `ifstream` object.

```cpp
// main.cpp
// Testing ifstream with >> and getline
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main()
{
    ifstream ifs;
    string my_line;

    ifs.open("test.txt");
    ifs >> my_line;
    cout << my_line << endl;

    getline(ifs, my_line);
    cout << my_line << endl;

    ifs >> my_line;
    cout << my_line << endl;

    return 0;
}
```


Expanded example, using a `while` loop:
```cpp
/// io.cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main()
{
    ifstream ifs;
    string my_line;

    ifs.open("test.txt");
    if (ifs.fail())
    {
        cerr << "Unable to open the file" << endl;
        exit(-1);
    }

    while (getline(ifs, my_line))
    {
        cout << my_line << endl;
        if (my_line == "line1")
        {
            cout << "Hello, line1" << endl;
        }

    }

    ifs.close();
    cout << "The End" << endl;

    return 0;
}
```

Contents of test.txt
        line1
        line 2
        line 3 and 4

        
# Midterm preparation

See the lecture slides for the list of topics on the exam, as well as the practice problems and solutions presented during lecture. 

### Here are some problems to expect:
**Note that this list is not comprehensive, and you should be comfortable with any material discussed in lectures, homeworks, and labs.**
---
* Code Tracing
	* Given a piece of code, determine its behavior or output

* Code Completion
	* Given a few lines of a program and its output, fill in the missing lines
	
* Bug Hunting:
	* Given a piece of code, find all the errors. We will tell you how many errors to look for.
	* Make sure to check edge cases and precedence or operations in loops and boolean statements
		* Edge cases = the extreme cases, such as the first and last numbers used in a loop
		
* Block Placement:
	* What is the proper order to place "blocks" of code in?
	* Notes on functions:
		* The declaration is function’s return value, name and parameters. The definition is its implementation (code). A declaration must appear before the function is ever called in the program, but the definition can appear anywhere. If you want to "combine" the declaration and definition, you can place the entire definition before the function is called anywhere in the code (you will no longer need a declaration)
			* The declaration and definition of a function share the same header, but the declaration is always followed by a semicolon.
    		* Important to decide whether it should return or print the result
    		* Decide whether the function will take arguments or not
			* If it does, place a list of the expected arguments in the parentheses that follow the function header
			* EX: `int count( int one, int two, int three)`
				* This is a function that takes three integer *arguments* and *returns* one integer value
    		* Remember to use a semicolon after a list of function’s arguments when writing the function *declaration*
   		* Functions can only access data inside its scope. If a variable uses some variable declared in another place, pass it as a parameter.

* Command-Line Arguments:
	* Be able to convert a program that does not take command-line arguments into one that requires command-line arguments. Know how to use `argc` and `argv` in your program.

Converting the example from the slides to accept the user input from the command line.
*Note that the program will crash if no additional command-line arguments (other than the name of the executable) are provided!*

```c++
// mult_cl.cpp
#include <iostream>
using namespace std;

int main(int argc, char *argv[])
{
    int sum = 0;
    int n = -1;

    n = atoi(argv[1]);

    for(int i = 1; i < n; i++)
    {
        if ((i % 3 == 0) || (i % 5 == 0))
        {
            sum += i;
        }
    }
    cout << "The sum is " << sum << endl;
    return 0;
}
```

### Miscellaneous
---
* How are booleans output? What if the value that takes the place of a boolean is not 1 or 0?
    * First, the expression is converted into a boolean. Everything that is not 0 is converted to a 1 (true), and 0 stays a 0 (zero). Boolean values are output as 1 (true) or 0 (false).

* Know your basic vim commands (mode switching, etc)

* Be familiar with information from the reading- just because it wasn’t on the homework doesn’t mean it’s not important to being a good programmer.

* Different types of errors, and how to identify them:
	* Compile-time: When a program fails to compile.
		* Syntax errors are a commong example of this- if you are missing a semicolon or a bracket {}, or have a misspelling somewhere that the compiler cannot understand, then the compilation will fail and no executable will be created.
	* Run-time errors: Using invalid operations in code
		* The compiler doesn't check if you are using valid data or operations when it creates the executable. Run time errors occur when your program crashes after trying to execute an invalid operation (dividing by 0, for example).	
	* Logic errors: Not the expected output
		* These errors are the trickiest to find, because the program compiles and runs normally but doesn't behave as it was intended to. Common logic errors are: Dividing by the wrong number (programming in the wrong math), being off by one in your loop indices (too high or too low), and mistakes in boolean logic (if-else statements, while-loop tests, etc)

* C++ doesn’t care about spacing/tabs/newlines, etc

* Functions are the most important section!
    - Don’t spend a disproportionate amount of time on the basics- be sure to review complex concepts
    - Be comfortable with programming concepts in the most recent lab and lecture (this Tuesday and Wednesday)

Converting the example from the slides to use a function and provide a more elaborate output:

```c++
// mult_funct_n.cpp
#include <iostream>
using namespace std;

int compute_sum(int limit)
{
    int sum = 0;

	for(int i = 1; i < limit; i++)
	{
		if ((i % 3 == 0) || (i % 5 == 0))
		{
			sum += i;
		}
	}

    return sum;
}

int main()
{
   int n = -1;
	cout << "Enter n: ";
	cin >> n;

    for (int i = 0; i < n; i++)
    {
        cout <<"i = " << i << " The sum is " << compute_sum(i) << endl;
    }
	return 0;
}
```


