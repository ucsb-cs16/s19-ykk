---
num: "lect06"
lecture_date: 2019-04-18
desc: "Loops, switch, functions + makefile"
ready: true
---

This lecture mainly focused on the following topics:

* `for` vs. `while` loops

* `switch` statement

* functions

* Makefile and `make`

The first example illustrated how `for` loop can be written using a `while` loop and highlighted the major things we need to keep in mind when writing a `while` loop.

```cpp
// main.cpp
#include <iostream>
using namespace std;

// A function to print the star * n times
void print_star( int n );

void print_star_while( int n );

int main()
{
    int n = 5;
    print_star(n);
    cout << " Now, with a while" << endl;
    print_star_while(n);

     return 0;
}

// A function to print the star * n times
void print_star( int n )
{
    for (int j = 0; j < n; j=j+2)
    {
        cout << endl;
        for (int i = 0 ; i < n; i++)
        {
            cout << "*";
        }
    }
    cout << endl;
}

void print_star_while( int n )
{

   int loop_cntr = 0;

    while ( loop_cntr < n)
    {
        cout << "*" ;
        ++loop_cntr;
    }
    cout << endl;
}
```

To trace though the code above, we used the following notes to count the values of the variables:
    j = 0   i = 0
    j = 0   i = 1
    ..
    j = 0   i = 4
    j = 2   i = 0
    j = 2   i = 1
    ...
    j = 2   i = 4
    j = 4   i = 0
    ...
    j = 4   i = 4
    j = 6

We wrapped up this example by writing a very simple Makefile for compiling and removing our `print_star` executable:

```
print_s: main.cpp
	g++ main.cpp -o print_star

clean:
	rm -f print_star *.out
```

To use this makefile, we can now type `make`, which by default always builds the first target in the makefile (in our case, it would be `print_s`).
`make clean` will find the `clean` target and execute its command, which would remove the executable and any `.out` files in the directory.

In general, a makefile rule has this structure:

    target_name: dependency_1 dependency_2 …
        command_to_make_target_1
        command2

-------

We then looked at how to write a `switch` statement and what happens when you don't include a `break` inside the `case` statements.

```cpp
// switch.cpp
#include <iostream>
#include <cstdlib>
using namespace std;

int main(int argc, char *argv[])
{
    char answer = 'y';

    answer = *(argv[1]);  // a dangerous move without checking argc first

    switch(answer)
    {
        case 'N':
        case 'n':
            cout << "You said No" << endl;
            break;
        case 'Y':
        case 'y':
            cout << "You said Yes" << endl;
            break;
        default:
            cout << "This is default" << endl;
            cout << "You said " << answer << endl;
            break;
    }
    return 0;
}
```

Another version, getting user input as part of the `while` loop:
```cpp

#include <iostream>
#include <cstdlib>
using namespace std;

int main()
{
    char answer = 'y';

    while (answer != 'q' && answer != 'Q')
    //while (answer != 'q' || answer != 'Q') // logic error; infinite loop
    {
        cin >> answer;
        switch(answer)
        {
            case 'N':
            case 'n':
                cout << "You said No" << endl;
               // break;
            case 'Y':
            case 'y':
                cout << "You said Yes" << endl;
                break;
            default:
                cout << "This is default" << endl;
                cout << "You said " << answer << endl;
                break;
        } // end switch
    } // end while

    return 0;  // Make sure this is outside of the while loop, otherwise, the program will exit too soon
}
```
# Practice Questions	https://docs.google.com/document/d/1j_J25q3XOB1M-zgpy1zvIPQVa4p_hx_QuqUGg6EADpE/edit#
1. Write a Makefile so that when we type `make hello`, the compiler will compile the file `main.cpp` into an executable named `program01`
2. Write the following if/else-if/else chain as a switch statement
```
char grade;
cin >> grade;
if(grade == ‘A’)
	cout << “Grade > 90%” << endl;
else if(grade == ‘B’)
	cout << “Grade > 80%” << endl;
else if(grade == ‘C’)
	cout << “Grade > 70%” << endl;
else
	cout << “Shamefur dispray” << endl; 
```
