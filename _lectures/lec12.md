---
num: "lect12"
lecture_date: 2019-05-09
desc: 
ready: true
pdfurl: 
---


# Recap

There are 3 different ways to pass a variable into a function

Let's look at how we could implement initBox() that takes a box and initializes its member variables to 0.

* Pass by value -- `void initBox(Box b)`

A local copy of a box will be created, any changes within the function are not applied to the original object passed in.
The local copy is lost after the function returns.

* Pass by reference -- `void initBox(Box& b)`

A reference (nickname) to an object is created. Memory management is highly efficient. Any changes to a local reference are applied to the original object as well. **Arrays are always passed by reference.**

* Pass by address (also called bass by pointer) -- `void initBox(Box* b)`

A pointer is created, which allows us to access the original object **through dereferencing**. Memory management is highly efficient.
If a box has a `width` member variable, access it either by `(*b).width` or `b->width`.


* A reminder about the asterisk operator (`*`)

When you use `*` to declare a variable, you are creating *a pointer of the specified type*:
`char* ch` -> ch is a pointer to a `char` variable

When you use `*` anywhere else, you are **dereferencing a pointer**
```
char* ch;
char c = 'a';
ch = &c;
*ch = 'b' // c now holds a 'b' inside.
```

### Pointers 

Pointers are data types just like ints or chars, but instead of numbers and characters, **a pointer stores a memory address**.

Write this down somewhere you can see it while you are programming, and keep referencing this statement:
**a pointer stores a memory address** (represented by a hexadecimal value).

To create a pointer, specify the type of an object that the pointer will point to and add an _asterisk_ (`*`).
```cpp
int a = 80;
cout << &a << endl; //0x2a8c64d78a0a
int* p; //p (a pointer to an integer) was created
p = &a; //p now stores the address of a.
cout << p << endl; //0x2a8c64d78a0a, same address as above
```

* Notice that we did not have to print `&p` to get the location of `a`. The pointer `p` already stores it as its value (because a pointer stores a memory address), just like `a` stores 80 as its value.

What can we do with pointers? Well, we can access the things they point to using the asterisk.
```cpp
int a = 80;
int* p = &a;
cout << p << endl; //0x2a8c64d78a0a
cout << *p << endl; //80
```

__This is very important__
* When you access `p`, you access **the memory address** stored in `p`
* When you access `*p`, you access **the value** stored **at the memory address** that is in `p` (the value stored in the variable whose memory location is stored in `p`).

This process of getting the value stored in memory, which is pointed to by the address stored inside a pointer, is called **_dereferencing_ a pointer**.

Look at the last example with `a` and `p`.
`*p` is equivalent to `a`.
Why? Because `p == (&a)`, so `*p == *(&a)`
This command is saying: "Get me the address of `a` (`&a`), and then get me what's stored at that address (`a`)"

Let's see how we can solve the same problem of swapping variables, this time, using pointers:

```cpp
// swap-ptr.cpp
#include <iostream>
using namespace std;

void swapValue(int* x, int* y){
    cout << "x = " << x << endl;  // address of a
    cout << "*x = " << *x << endl; // value stored at a
    cout << "y = " << y << endl; // address of b
    cout << "*y = " << *y << endl; // value stored at b
    cout<< "&x = " << &x <<"  "<< "&y = " << &y <<endl;
    // the above line prints the address of the *pointers* x and y
    // note that their addresses are different from the *values* (which are addresses) stored at x and y
    // remember that the addresses of a and b that we printed are the *values*/addresses stored at x and y
    
    int tmp = *x; //tmp stores 30
    *x = *y;
    *y = tmp;
}

int main() {
    int a=30, b=40;
    cout << "=== Before the swap ===" << endl;
    cout<< a <<"  "<< b <<endl;
    swapValue( &a, &b); //passing LOCATIONS OF a and b
    cout << "=== After the swap ===" << endl;
    cout<< a <<"  "<< b <<endl;
    cout<< "&a = " << &a <<"  "<< "&b = " << &b <<endl;
}
```

The following assignments took place "under the hood" during the call to `swapValue`:
```cpp
int* x = &a;
int* y = &b;
```

We accessed the values stored in `a` and `b` by *dereferencing* `x` and `y` pointers, which store the locations of `a` and `b` respectively.


Let's pause and review what we've learned:
* Pointers store locations/addresses of variables
* To create pointers, you need to specify the type of object it will point to (int, char, string), and use the asterisk sign (`*`)
* To store a variable's location, use the ampersand sign (`&`) from earlier:
```cpp
int* p = a; //p is a pointer to a, p stores a's location
```
* Pointers CAN change what they point to!
```cpp
int a = 10, c = 9;
int* p; //p (pointer) was just created
p = &a; //p points to a
cout << "*p: " << *p << endl; //10
p = &c; //p now points to c
cout << "*p: " << *p << endl; //9
```


Make sure this also makes sense and you understand when to use `&` and `*`, and what vaue each would provide.


## Pointers and arrays

When we learned about arrays, we promised to come back to them once we've leanred about pointers. Here we are.
The variable declared as an array is actually just a pointer to the first element.
```cpp
int arr[] = {5,4,3}; // arr points to the first element (currently 5)
cout << arr << endl; //0x2a8c64d78a14
cout << &(arr[0]) << endl; // same as `arr`, 0x2a8c64d78a14
```
Note that when you run the above code, you will get different values, because the compiler will assign variables to different memory locations.

* To get *the first element* of the array, we would type arr[0];
  * This is equivalent to *arr
* To get *the second element*, we would type arr[1];
  * This is equivalent to *(arr+1)
  * This is what is called **pointer arithmetic**, and it is used to get to other locations around the given starting point.
* When we learned about arrays, we said that it was important that all elements in an array were adjacent in memory. This is why: only in this case using pointer arithmetic helps us traverse through an array. 

* For those of you who want to know the specifics:
  * Remember how value of `arr` in the code above was 0x2a8c64d78a14?
  * This tells us that the first element is at location 0x2a8c64d78a14.
  * The size of one integer is 4 bytes, so the second element is at location 0x2a8c64d78a18.
  * The third element of arr is at location 0x2a8c64d78a1c (hexadecimal addition: 18 -> 19 -> 1a -> 1b -> 1c)

* Final notes on pointers:
  * When pointers are **declared**, they hold **junk values**. Defererencing (i.e., using `*`) such pointers is dangerous, because their values are not properly initialized, which means that they do not hold the valid memory location. It might, depending on what's inside, tamper with your data, or attempt to reach something that the pointer doesn't have access to, causing a segmentation fault.
  * The best solution is to always initialize your pointer to `NULL` (`int* p = NULL;` or `int* p = 0;`)
  * Pointers are used to travel to a different world called "heap" that we are going to talk about later in the course.
  * We will be using pointers a lot, so it is important that you are comfortable switching between using *the value* stored in the pointer vs the value *stored at the location* that is stored in the pointer.

## Final notes

Pointers and references are confusing! They are arguably the hardest topic of the course, and are used a lot in C++.
They are not intuitive, and may not make sense at first. That's okay. We will be using them a lot, and it will get better. Use the resourses you have, including these notes and slides, and ask for help. Don't wait until the week of the midterm.

**Key concepts**:
* A **pointer stores a memory address** (represented by a hexadecimal value). 
* To access an address/reference, use the ampersand `&`
* To **dereference a pointer** use an asterisk `*`; doing so will access **the value** stored **at the memory address** that is stored by the pointer
