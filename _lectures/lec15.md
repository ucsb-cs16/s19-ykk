---
num: "lect15"
lecture_date: 2019-05-28
desc: String and recursion
ready: true
reading: Section 8.1-8.2, Chapter 14 
---

# Link to slides
<https://drive.google.com/drive/folders/1zP7YNmZXCYnAP8MrEiaf1Ov28ESpXR0s>

# C-Strings

Strings are characters in a sequence.

We've previously used `string` before. However, since C++ is based on C, you can also use an array of characters to represent a string. In fact, this was how C represented strings.
* This is refered to as a C-string
* Just like the library <string>, C++ has a <cstring> library, that includes built-in functions that go with C-strings
* C-strings and character arrays are slightly different, in that a C-string has a character called the null-terminator at the end of the string. This terminates the actual string, but not necessarily the array part of the C-string.
  
Even though the <string> class contains more functionality, C-strings are still used very often.

Recall: Command-line arguments
* Remember that in command-line arguments, `argv[x]` was defined as `char*[]`
* This is a C-string, therefore we have to treat `argv[x]` as C-strings and their corresponding functionality

To declare a C-string, include `<cstring>`, and use the following syntax:
```
char myCString[sizeWeWant + 1];
```
We add 1 to the size, to reserve the space for the Null terminator

Downsides to C-strings:
* We cannot use = to assign a C-string to another C-string
* We cannot use == to check if a C-string is equal to another C-string
```
...
const int C_STRING_SIZE = 5;
char cStringExample[C_STRING_SIZE + 1] = "hello";
char cStringSecondExample[C_STRING_SIZE + 1] = "olleh; 

char cStringThirdExample[] = "wasd keys;   //Like arrays, we don't have to explicitly specify a size in the brackets

// cStringSecondExample = cStringExample;     //This is not allowed
// bool testEqual = (cStringSecondExample == cStringExample);   //This is also not allowed

//However, we could do this
strncpy(cStringSecondExample, cStringExample, 6);

//And this
bool testEqual = strncmp(cStringSecondExample, cStringExample, 6);
...
```

# Strings
We don't have the limitations of C-strings if we are using strings instead

To declare strings, first include `<string>`
You can declare them now like `string x = "hello world";`

Since strings are made of characters, you can access them like an array
```
string x = "hello world";
char zero = x[0];   //this stores 'h'
char two = x[4];    //this stores 'o'
```

To get the size of a string, you can do `.size()` or `.length()`
They are the exact same, although you'll find `.size()` with other C++ standard library classes, but not `.length()`

# Character processing
There are many pre-defined functions that deal with characters, in the `cctype` library
To use it, include `<cctype>`

Here are some of the following
* toupper: returns an uppercase version of the argume t
  - `toupper('a')` returns 'A'
  - `toupper('A')` returns 'A'
* tolower: same as toupper, but lowercase instead
* isspace: returns true if the argument is a whitespace (spaces, tabs, newlines)
  - `bool x = isspace(' '); //x should be true`

# String processing
Like Python, we can concatenate strings (concatenate is just a fancy word for adding strings together to form longer strings)
```
string a = "Hello ";
string b = "World!";
string c = a + b;
cout << c << endl;  //will print Hello World!
```

Just like adding numbers, `+=` allows you to append strings
```
string a = "Hello";
string b = "!";
a += b
cout << a << endl;  //will print Hello!
```

Here are some more string functions
* Search: find, rfind, find_first_of, find_first_not_of
* Size: length, size
* String content access: substr, replace, append, insert, erase

## The find functions:
Checks if a string contains a specific string. This function will return `string::npos` if there are no occurrences. Otherwise, it will return the index of the 1st occurrence.

`find()` can accept a 2nd parameter that you can specify, to tell `find()` the index to start searching.

An alternative to `find()`, `rfind()`, searches for the last occurrence.

find_first_of() returns the 1st occurrence of any of the characters included in the specified strings
find_first_not_of() finds the 1st occurrence of a character that's not any of the characters included in the specified string

## The append function:
You can use `append()` to append strings to other strings. This function serves the same function as string concatenation.

## The erase function:
Without any parameters, the `erase()` function turns a string into an empty string.

It can also take in 2 parameters, the 1st parameter as the index you want to start erasing, and the 2nd parameter as how many places after the starting index to erase

## The substr function:
The substring function, `substr()`, takes in 2 parameters

If you give it 1 parameter, the starting index, it returns a string starting from the index

If you give it 2 parameters, the 1st is the starting index, the 2nd is how many letters from the starting index you want to "preserve"

## The sort function
Unlike other functions, you don't call sort() on a string
```
string x = "wasd";
x.sort()    //DON'T DO THIS
```
sort() is part of the standard library, and accepts 3 parameters.

In the case of strings, if you want to sort the entire string, you would use the following syntax:
```
string h = "hello";
std::sort(h.begin(), h.end());  //this modifies the string h directly
```

# Intro to recursion
Recursive functions call itself

More accurately, a recursive algorithm divides itself into smaller versions of itself
For example: an array of size x can be described as a single element and a subarray of size x-1

Any recursive implementation can also be done without recursion, using loops (recursive vs iterative solution)

For any recursive implementation, we first start with a base case:
* What is the simplest scenario? Are there multiple base case scenarios?
* After implementing the base case, we then think about the recursive call part

**Benefits of recursion**: Recursive implementations can be significantly simpler in terms of code than iterative implementations

**Downsides of recursion**: Recursion can take up tons of space, and can be really inefficient if the input is very big

Without a proper base case, we can have inifinite recursion.
This can cause the recursion to grow beyond the limit of the stack, leading to stack overflow (no, this is the BAD stack overflow), and causes the program to crash.

