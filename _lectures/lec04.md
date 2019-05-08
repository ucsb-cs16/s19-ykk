---
num: "lect04"
lecture_date: 2019-04-11
desc: "User input/output and loops"
ready: true
reading: Chapter 3
---


## User Input and Output

* **`<<`** is an insertion operator used with the _output stream_ and always goes together with the `cout`
* separates expressions of the _same type_.

You can ‘cascade' the insertion operators, rather than using another `cout` command when printing

```c++
	cout<< "Hello, my name is ";
	cout<< name << endl;
```

Can be written as

```c++
	cout<< "Hello, my name is "<< name << endl;
```


To collect user input, the _input stream_ uses **`>>`**, _the extraction operator_.
The extraction operator **`>>`** is used with **`cin`** to store user input:

```c++
int num = -99;
cout << "Select a number between 0 and 100 (inclusive): ";
cin >> num;
cout << "You selected " << num << endl;
```

* In the above code, create a variable to hold the input (`int num`).
* Take input from terminal, store in that variable (`cin >> num`). No input is collected until you press ENTER.

Once the input is taken, can't directly see what is stored in the variable.
Good practice is to print it out to display and check.

Make sure that input is being stored in a variable of appropriate type.
No strings stored in integer vars, etc.
Sometimes inputs can be stored as different types, but might not behave as expected.
A number can be stored as a string, but you wouldn't be able to do math with that number as you would with an int (it will behave as a string).

Use `if else` statements to check for conditions of input variables to produce different outputs based on the values entered by the user.


### Newline (a "carriage return" character)

The placement of `endl` controls where the new line appears on the screen:
* If `endl` is included before the output (e.g., before `num`), then the text will appear on the next line. 
* If `endl` is included after the output, the text will appear on the same line and whatever comes after, will be on the next line.
* `endl` is included after the `<<`
* `\n` is included **inside the quotations** of a string output

_Read the discussion in the book about the style choice of using `\n` vs. `endl` to add a **carriage return**._
`\n` (which is a _single_ character) is the same as `endl`.
Savitch's recommendation: use `\n` when the last thing printed was a string, `endl` when last thing was a variable (in general).


## Coding Process

Edit, Compile, Run until program produces the correct behavior.

**Compilation**

Executable file name defaults to `a.out`, if no name is specified, the compiler doesn't know where to store the output.
Compiling a different file with no executable name will overwrite an existing `a.out`.

When compiling a file for the first time
* If the compiler encounters an error, no executable code is generated
* If you fix mistake and recompile, an executable will be produced

Compiling the same file further in development
* If a compiler encounters an error at this stage, the previous executable will still exist but **will not** be updated- will not reflect changes made to the .cpp file.
* Compilation must include the `-o` flag in the `g++` command to indicate that the executable should be stored in a file with the chosen name.


*PRO TIP*: If a program is stuck in an infinite loop, `CTRL+C` breaks the execution.

*PRO TIP* (Good debugging technique): ERRORS: Don't look at the bottom of the list of errors, look at the top for the very first error - addressing that error might fix all others.


## Initialization vs. declaration

Know your terminology and use it correctly!

Without initialization, it's just a **declaration** of a new variable, e.g., `int i`;

When you declare without initializing, you create a space in memory for the value, but you don't assign anything to that space.
This often means that an unintialized variable holds garbage values until it is assigned, so it can be dangerous to perform operations until it is initialized.
For example, `string str`; //by default the string class sets it to an empty string, but depending on the compiles, it may not.

When you declare a variable and immediately assign it an _initial_ value, then you have _initialized_ it.

```c++
	int age = -99;
```
or

```c++
	int age;
	age = -99;
```

*PRO TIP*: Initializing a variable to a dummy value outside the normal range might make it easier to debug later.

*PRO TIP* / Personal preference: declare all variables at the top of the file to see clearly which ones are `int` or `string`, etc., even if they are used later on.




# Control Structures: Loops

## `while` loop

A while loop is used to repeat code while some condition is true.
```c++
	while(BOOLEAN_EXPRESSION) {
		// Code to run when the BOOLEAN_EXPRESSION is true.
	}
```

Check if the BOOLEAN_EXPRESSION is true.
* If true, the statements inside the loop's block will execute.
* at the end of the loop block, go back to `while`.
* If false, the statements in the loop will not execute.
* the program execution after the loop continues.

Example usage: say we want users to enter a non-negative number.
Use a while loop, so that users must keep entering values until the boolean statement is satisfied
```c++
    while(num < 0) {
    	//keep asking user, taking in input
    }
```

## Example

```
int i = 0;
while (i < 10)
	cout << "i = " << i << endl;
	// add i++ afterwards to eliminate an infinite loop.
	// i++ → i = i + 1;
	// Remember to enclose this statement with { }
```

* Note that a single statement after a while loop (similar to an if statement) is considered part of the loop without the { }.
	* If more than one statement is part of the loop, this must be contained within the { }


The boolean statement is checked first, and the body is skipped if the requirements are met.
Once the bool statement (`num < 0`) is no longer true, i.e., the user provided a non-negative number, the loop will stop.


The `while` loop has two flavors: a usual `while` that we looked at above, and `do-while` loop, which is used when the body of the loop needs to be executed **at least once**.

## `do-while` loops

A `while` loop is used to repeat code once and then until some condition is no longer true:

```c++
	do {
		// Code
		// This code is executed once
		// and is executed again if the BOOLEAN_EXPRESSION below is true
	} while(BOOLEAN_EXPRESSION);
```

1. Execute the code in the loop
2. Check if BOOLEAN_EXPRESSION is true.
* If true, then go back to 1.
* If false, then exit the loop and resume program execution.

Note: You must have a semicolon (`;`) after the `while` statement, if you are using a `do-while` loop (no semicolon if it is just a `while`).

In all loops, remember to **update the variable controlling the loop each time** (examined in bool test), otherwise an infinite loop will occur.
After any while loop, we know that the variable being examined meets a particular condition (e.g., `num >= 0`), otherwise, we would not have exited the loop.

## Example

```
int i = 0;
do {
	cout << "i = " << i << endl;
	i++;
} while (i < 0);
```

* Outputs "i = 0" once regardless of what the BOOLEAN_EXPRESSION evaluates to.
* Change to `while (i < 10)` to print "i = [0 - 9]".


## `for` loops

The `while` and `for` loops can be interchanged, but some formats are more convenient than others in different situations.

The `for` loop is used to repeat code (usually a fixed number of times).

```c++
	for (INITIALIZATION; BOOLEAN_EXPRESSION; UPDATE) {
		// Code to run when the BOOLEAN_EXPRESSION is true.
	}
```

1. Execute the INITIALIZATION statement.
2. Check if the BOOLEAN_EXPRESSION is true.
* if true, execute code in the loop.
* THEN execute UPDATE statement.
* Go back to the BOOLEAN_EXPRESSION.
* if false, do not execute code in the loop.
* exit the loop and resume program execution.

## Example

```
for (int i = 0; i < 10; i++) {
	cout << “i = “ << i << endl;
}
```

## Nested Loops

Other loops within a loop can be defined.

## Example

```
for (int i = 0; i < 5; i++) {
	cout << “—“ << endl;
	cout << “i = “ << i << endl;
	for (int j = 0; j < 5; j++) {
		cout << “j = “ << j << endl;
	}
}
```



### Skipping and Terminating Loop Execution

`continue`
* Once a `continue` line is reached, go back to the top of the loop immediately

`break`
* Once a `break` line is reached, the program will _exit_ (break out of) the loop immediately

In both cases, the program ignores anything else in the block that comes after continue/break,
i.e., the rest of that block below the `continue`/`break` line is **not** executed

## Example

```
for (int i = 0; i < 10; i++) {
	if (i == 4)
		continue;
	if (i == 7)
		break;
	cout << “i = “ << i << endl;
}
```



# Formatting output to the terminal

* Several ways to do this.
* We can customize the `cout` function to display floating point numbers as follows:

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2); // prints two decimal spaces for floating point values.
```	

# Example: A number guessing game

```
#include <iostream>

using namespace std;

const int ANSWER = 42; // const values cannot be modified

int main(int argc, char *argv[]) {

	int input = 0;

	do {
		cout << "Guess a number between [0 - 100]: ";
		cin >> input;
		if (input == -1)
			break;
		if (input < ANSWER) {
			cout << "Too small" << endl;
			continue;
		}
		if (input > ANSWER) {
			cout << "Too big" << endl;
			continue;
		}
		if (input == ANSWER) {
			cout << "WINNER! ANSWER = " << ANSWER << endl;
			break;
		}
	} while (true);

	cout << "Thanks for playing!" << endl;
}
```

**Math Puzzle**
One of the powers of computing is being able to do a brute-force search for a solution to a problem. Trial and error works just fine for some problems. In fact, computers can be especially good at such problems. Consider this:

Horses cost $10, pigs cost $3, and rabbits are only $0.50. A farmer buys 100 animals for $100, How many of each animal did he buy?  

Write a program to do this.



## Code written during lecture

The final file (without the intermediate changes):

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main(int argc, char* argv[])
{
    int int1 = -1;
    int int2 = -1;

/*
    for (int i = 0; i < 10; i++) {
        if (i == 4)
            continue;
        if (i == 7)
            break;
        cout << "i = " << i << endl;
    }
*/
    cout << "Enter two numbers: ";
    cin >>  int1 >> int2;
    while (int1 == int2)
    {
        cout << "int1 = " << int1 << endl;
        cout << "int2 = " << int2 << endl;
        cin >>  int1 >> int2;
    }

    cout << " Now, with the do-while" << endl;

    do {
        cout << "int1 = " << int1 << endl;
        cout << "int2 = " << int2 << endl;
        cin >>  int1 >> int2;
        if (int1 == int2)
        {
            break;
            cout << "I love " << int1 << endl;
        }
    }
    while (int1 == int2);

    return 0;
}
```
# Practice Questions
1. Write the following `for` loop as a `while` loop. Assume the code snippet below is properly implemented in a working C++ program.
```
int x = 0;
for(int i = 0; i < 10; i++){
	x++;
}
```
2. In what scenarios would you use a `do-while` loop?
