---
num: "lect10"
lecture_date: 2019-05-02
desc: "Structs"
ready: true
reading: "Section 10.1"
---


Helpful online visualization of C++ programs (may help to understand pointers): [http://pythontutor.com/cpp.html#mode=edit]

## Structs

* A bunch of variables that, taken together, describe an object 
  * Structs are a simple **data structure**
  * The member variables are initialized in curly braces (in the order they are listed in the struct).
* **Example struct syntax:**
```
struct Name{
    String first;
    String last;
};
```
* **Remember the semicolon at the end of the struct definition!**
* To access member variables, use the dot operator `.`
  * **EX:** 
  ```
    Name n = {"Harry", "Potter"};
    cout<< n.first; //prints "Harry"
  ```
* Accessing member variables allows you to print, compare, or change the values of those mem vars
* If one of the member variables is also a struct, use the dot operator once more to access the member variables of that struct 

## Diagrams
* [Example visualization diagram](https://docs.google.com/presentation/d/1Y7J2i2WfoOc_WAclsPcGzsHJklG9aUkSVSchWySBCls/edit?usp=sharing)


# Code from lecture

```cpp
//print_student.cpp

#include <iostream>
#include <string>
using namespace std;

struct Student {
    string fname;
    string lname;
};

void print_student( Student s);
// Precondition: Student s has been initialized
// Postcondition: Student information is printed
// one value on each line

int main()
{
    Student student1;
    Student student2;
    Student student3;
    Student &s_ref = student2;

    student1.fname = "Hermione";
    student1.lname = "Granger";
    student2.fname = "Harry";
    student2.lname = "Potter";

    //cout << student1.fname << endl;
    //cout << student1.lname << endl;
    print_student(student1);

    cout << s_ref.fname << endl;
    s_ref.fname = "Ron";
    cout << s_ref.fname << endl;

    print_student(student2);


    return 0;
}

void print_student( Student s)
// Precondition: Student s has been initialized
// Postcondition: Student information is printed
// one value on each line
{
    cout << s.fname << endl;
    cout << s.lname << endl;
}
```

Pass the struct by reference to set its variables

```cpp
// init_student.cpp


#include <iostream>
#include <string>
using namespace std;

struct Student {
    string fname;
    string lname;
};

void print_student( Student s);
// Precondition: Student s has been initialized
// Postcondition: Student information is printed
// one value on each line

void init_student(Student &s, string first, string last);
// Precondition: Student s is declared
// Postcondition: s.fname is set to "first", last name is assigned to s.lname

int main()
{
    Student student1;
    Student student2;
    Student student3;
    Student &s_ref = student2;

    /*
    student1.fname = "Hermione";
    student1.lname = "Granger";
    student2.fname = "Harry";
    student2.lname = "Potter";
    */
    init_student(student1, "Hermione", "Grager");
    init_student(student2, "Harry", "Potter");

    //cout << student1.fname << endl;
    //cout << student1.lname << endl;
    cout << "from main" << endl;
    print_student(student1);
   /*
    cout << s_ref.fname << endl;
    s_ref.fname = "Ron";
    cout << s_ref.fname << endl;
    */
    print_student(student2);


    return 0;
}

void print_student( Student s)
// Precondition: Student s has been initialized
// Postcondition: Student information is printed
// one value on each line
{
    cout << s.fname << endl;
    cout << s.lname << endl;
}

void init_student(Student &s, string first, string last)
// Precondition: Student s is declared
// Postcondition: s.fname is set to "first", last name is assigned to s.lname
{
    s.fname = first;
    s.lname = last;

    cout << "from init_student" << endl;
    print_student(s);
    return;
}
```

Partial example with coordinates

```cpp
#include <iostream>
using namespace std;

struct Coord {
    int x;
    int y;
};

struct Box {
    int width;
    int height;
    Coord upper_left;
};

struct BigBox {
    int bb_width;
    int bb_height;
    Box inner_box;
    Box outer_box;
};

int main()
{

    Coord coord1 = {4,3};

    Box b1 = {22, 33, coord1};
    Box b2 = {44, 55, {1,7}};

    BigBox bb;

    b1.width = 2;
    b1.height = 3;
    b1.upper_left.x = 1;
    b1.upper_left.y = 2;

    return 0;
}
```

