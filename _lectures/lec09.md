---
num: "lect09"
lecture_date: 2019-05-02
desc: "Passing Parameters to functions; Numerical base conversions"
ready: true
reading: Sections 5.2-5.3 + slides
---

From now on, include pre- and post- conditions for the functions that you write:
    * Precondition: What you expect the function to receive
    * Poscondition: What you expect will be true once the function has completed
    * These should be added as a pair of comments right before each function
    * *If you update your function*, make sure to read over your pre- and post- conditions to make sure they still make sense and match the new code. Update them if necessary as you edit your code.
    
# Code from Lecture


First, we wrote a simple function to swap the values of two variables. This example motivates the need for the pass-by-reference mechanism, since we cannot `return` more than one value from a function.

```cpp
// Lecture 9 functions
// Pass-by-value vs. pass-by-reference

#include <iostream>
using namespace std;

void swap(int& val1, int& val2);
// A function to swap two integers
// Precondition: val1 and val2 are integers
// Postcondition: val1 has the value of val2
// and vice versa

int main()
{
    //int size = 3;
    //int arr[size];
    /* Declaring a function inside of another function leads to an error
void swap1(int& val1, int& val2)
{
    cout << "Hi from swap1";
}
*/

    int num1, num2;
    cout << "Enter 2 numbers: ";
    cin >> num1 >> num2;
    cout << "Num1 = " << num1 << endl;
    cout << "Num2 = " << num2 << endl;

    swap(num1, num2);
    //swap1(num1, num2);

    cout << "Num1 = " << num1 << endl;
    cout << "Num2 = " << num2 << endl;

    return 0;
}
void swap(int& val1, int& val2)
// A function to swap two integers
// Precondition: val1 and val2 are integers
// Postcondition: val1 has the value of val2
// and vice versa
{
    int temp = val1;
    cout << "---" << endl;
    cout << "Val1 = " << val1 << endl;
    cout << "Val2 = " << val2 << endl;
    val1 = val2;
    val2 = temp;
    cout << "Val1 = " << val1 << endl;
    cout << "Val2 = " << val2 << endl;
    cout << "---" << endl;
    //main();
}
```

We then use the `&` symbol that allows us to print the addresses of the variables to see the effect of pass-by-value (the values are copied into a different address) vs. pass-by-reference (the function uses the values stored at the same address that they were in the `main` function).

```cpp
// Lecture 9 functions

#include <iostream>
using namespace std;

//void swap(int &val1, int &val2);
void swap(int val1, int val2);
// A function to swap two integers
// Precondition: val1 and val2 are integers
// Postcondition: val1 has the value of val2
// and vice versa

int main()
{
    int num1, num2;
    cout << "Enter 2 numbers: ";
    cin >> num1 >> num2;
    cout << "Num1 = " << num1 << endl;
    cout << "Num2 = " << num2 << endl;
    cout << "num2& = " << &num1 << endl;
    cout << "Num2& = " << &num2 << endl;

    swap(num1, num2);  // The address locations change, depending on the formal parameters

    cout << "Num1 = " << num1 << endl;
    cout << "Num2 = " << num2 << endl;
    cout << "num2& = " << &num1 << endl;
    cout << "Num2& = " << &num2 << endl;

    return 0;
}
//void swap(int &val1, int &val2)
void swap(int val1, int val2)
// A function to swap two integers
// Precondition: val1 and val2 are integers
// Postcondition: val1 has the value of val2
// and vice versa
{
    int temp = val1;
    cout << "---" << endl;
    cout << "Val1 = " << val1 << endl;
    cout << "Val2 = " << val2 << endl;
    val1 = val2;
    val2 = temp;
    cout << "Val1 = " << val1 << endl;
    cout << "Val2 = " << val2 << endl;
    cout << "Val1& = " << &val1 << endl;
    cout << "Val2& = " << &val2 << endl;
    cout << "---" << endl;
    //main(); // fun test to see the infinite recursion
}
```

 ## Counting Numbers in Different Numerical Bases:
 * Computers count in base-2 (binary→ 0s and 1s), but we count in base-10 (decimal→ 0-9). This is because bits on hardware are easily represented in binary- they are tiny switches that are either on or off.
 * Other 2-related bases for counting in are:
   * Octal- base-8→ 3 bits (2<sup>3</sup> = 8)  (0-7)
   * Hexadecimal- base-16 → 4 bits (2<sup>4</sup> = 16) (0-9, A-F)
     * `A=10, B=11, C=12, D=13, E=14, F=15`

### Positional Notation 
* In **Decimal**:
  * Each position corresponds to a different power of 10
    * 642 = (6\*10<sup>2</sup>) + (4\*10<sup>1</sup>) + (2\*10<sup>0</sup>)
* Using the same principle, we can convert from **any** base into decimal 
  * What is 642 in base-13??
  * Each position is a power of 13
  * (6\*13<sup>2</sup>)+(4\*13<sup>1</sup>)+(2\*10<sup>0</sup>) = 1063
 
### **Converting Binary to Decimal**
 * What is 1011 (base-2) in decimal?
    * Start with the rightmost digit, 2<sup>(0)</sup>, and move up, multiplying by a larger power of 2 every time.
      * 1\*(2<sup>3</sup>) + 0\*(2<sup>2</sup>) + 1\*(2^<sup>1</sup>) + 1\*(2<sup>0</sup>) = 8 + 0 + 2 + 1 = 11
 * What if you add a bit to most significant end?
    * Now the binary number is: 11011 (which is 10000 + 1011 in binary)
    * Perform the same operations, but add 1\*(2<sup>4</sup>) = 16
      * 16+11 = 27
  
### **Converting Binary to Octal or Hexadecimal**
* Group the bits!
  * For octal, group the bits in the binary number by 3, starting from least significant (far right)
    * Because binary is base-2, and octal is base-8, which is 2<sup>3</sup>
  * For hex, group by 4s from far right
    * Because binary is base-2, and hex is base-16, which is 2<sup>4</sup>
  * Examples on slides!

### **Algorithm for converting Base-10 to other bases**
 * Available on slides in much greater detail (with examples)
    * Overview for **binary** example:
      * Divide decimal number by 2- the remainder will be 0 or 1
       * Add this to the left as the most significant bit of the the binary number you are producing
       * Divide the remaining “half” by 2, repeat w remainder, etc  until remainder is 0
       * The string of 1s and 0s you have produced from the remainders is the binary conversion
    * This process can be done with **any** number base- just divide by that base number repeatedly, rather than by 2
  
### **Why is this useful?**
  * Basics of memory manipulation and understanding
  * This is how everything is represented in memory
  * “Reverse engineering” of binary representations of objects
  * Pointers access, use, trade memory addresses
  * Memory addresses are *hex values*
  * You will be using hexadecimals when you assign pointers.
  
# Practice Questions
1. What does the following code print out?
```
void foo(int& x){
   x++;
}
int main(){
   int a = 5;
   foo(a);
   cout << a << endl;
   return 0;
}
```
2. Convert the decimal number 166 into hexadecimal and binary
