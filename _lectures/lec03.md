---
num: "lect03"
lecture_date: 2019-04-09
desc: "Variables and types, expressions, control structures (if-else), output"
ready: true
reading: "Chapter 2"
pdfurl: 
---

# CSIL

This is the guide on how to SSH into CSIL, so you can work from your laptop away from any COE computers
https://ucsb-cs16.github.io/topics/ssh_connect/

# Github Repos

* For the guide on creating your Github repo under our class organization, go to https://ucsb-cs16.github.io/topics/github_com_create_private_repo_under_org/
* Once you have created a repo, follow this guide to clone your repo in CSIL: https://ucsb-cs16.github.io/topics/git_cloning_your_first_repo/
* For a thourough guide on Git commands in CSIL for your repo, go to this guide: https://ucsb-cs16.github.io/topics/git_basic_workflow/
* If you want to avoid typing your Github login credentials everytime, follow this guide to setup SSH keys: https://ucsb-cs16.github.io/topics/github_ssh_keys/

## This segment only serves as a demo/reference, and does not represent the full features of Github

* Use `git clone <insert your repo HTTPS URL>`to clone your repo from Github to CSIL
* Use `git add <filename>` to add to the files you want to commit (update) to your github repo
* Note: if you add a non-Github repo, it will throw an error
* If you want to update all the files, you can use `git add .`
* `git status` shows any changes made that are ready to be committed
* `git diff` shows actual changes

* Use `git commit -m "<insert message here>"` to commit to your Github repo. The `-m` flag is to indicate a commit message, and the string represents the commit message for your commit (remember to include the double quotes)
* If you don't include the `-m` flag, and simply enter `git commit`, Git will open up the default text editor (Vim) for you to enter a commit message

* `git push` will push the changes committed to Github

# C++ Variables and Types

* Variables are used to store data.
  * Each variable must have a type associated with it.
    * Not the case in Python where a variable can be anything
    * Depending on the type, a variable occupies a different amount of bytes on disk
    * Smallest memory size is 8 bits or one byte
    * A variable's type also helps the compiler check that you are using the variable in an acceptable way (e.g., assigning a valid value)
  * Variable names must
    * Start with an alphabetical character or underscore (the latter is not recommended, since it's reserved for special cases, such as special library variables)
    * Other characters can be alphanumeric and underscore characters, but no spaces or other special characters.
  * C++ is *case-sensitive*. `x` and `X` are considered to be different variables.
    * I recommend _not_ using the camel-case notation that the book is using, and instead adopt a C-style naming convention that uses underscores.

* Some common types:
  * `int`: Integers
  * `double`: Floating point
  * `char`: characters (a single letter or symbol; values are always inside the single quotes, e.g., 'a' or '?')
  * `string`: sequence (array) of characters (strings are always inside the double quotes, e.g., "Hello!")
  * `bool`: boolean

* Good practice to initialize your variables
  * Uninitialized variables may have strange side-effects, e.g., running the same code with the same input but getting different answers.

    C++ programs are guided by rules, but undefined variable protocols are usually set by developers.
Some platforms may default undefined vars to 0, others might default to garbage vals (more common);
Can be a source of tricky bugs.

_PRO TIP_: initialize variable to a value that doesn’t make sense, so you can determined when it is not being set to the expected value later in the code.
For example, if 0 was an acceptable value, then you may not notice there was an error.

_PRO TIP / Best practice_: make your variable names relevant to what they do (random names for your variables is a big NO-NO).
Naming them with something that indicates what the variable is used for makes your code mode readable and maintainable.

_C++ shortcut_: 
To increment the value of a numeric variable by 1, simply add ++ to it. E.g.,
```c++
                    int count = 7;
                    count++; //count is now 8!
```
which is the shortcut for
```c++
                    int count = 7;
                    count = count + 1; //count is now 8!
```
also a shortcut
```c++
                    int count = 7;
                    count += 1; //count is now 8!
```



# Initializing, Assigning, and Modifying Variables

* Example

```c++
int x;      // declare variable x of type int
int y, z;   // declare variables x and y in one statement
x = 10;     // assign x to an integer value 10.

int a = 10;   // declare and initialize (i.e., assign its initial value) in one statement
int b = 20, c = 30;

b = 6 + 4;

cout << a << "," << b << "," << c << "," <<
x << "," << y << "," << z << endl;
```

* Operations between 2 double variables results in a double variable
* Operations between a double and an int variable still results in a double variable
* However, if you have an int variable, any decimals are automatically truncated

```c++
//which means
int x = 12.345;
cout << x << endl;  //will print out 12
```
* Or in this case:

```C++
double x = 1.2;
double y = 2.3;
int z = x + y;
cout << z << endl;  //will print out 3
```
* Different C++ compilers handle division by zero differently, some may just assign the "inf" (infinity) value, while some actually throws an error

# Boolean Expressions
* An expression that evaluates to either `true` or `false`.
* You can build boolean expressions with relational operators comparing values:

```c++
==  // true if two values are equivalent
!=  // true if two values are not equivalent
< // true if left value is less than the right value
<=  // true if left value is less than OR EQUAL to the right value
> // true if left value is greater than the right value
>=  // true if left value is greater than OR EQUAL to the right value
```

* Integer values can be used as boolean values
  * C++ will treat the number 0 as false and *any* non-zero number as true.

```c++
bool x = 5 == 1;  // x = 0
bool x = 3 != 2;  // x = 1
```

  * Combine boolean expressions using Logical Operators

```
!   // inverts true to false or false to true
&&  // boolean AND; Returns false if either expression is false, e.g., "false && true" returns false; otherwise, returns true
||  // boolean OR; Returns true if either expression is true, e.g., "false && true" returns true; otherwise, returns false
```
  
  * Example

```c++
bool x = true;
bool y = true;
x = !x;     // x = false
x = x && y    // x = false
x = x || y    // x = true
```

# Control Structures

* Boolean expressions are fundamental pieces that provide control flow within your program.

## If-else statements

* Ability to execute two alternative blocks of C++ statements based on the value of a boolean expression.

```c++
if (BOOLEAN_EXPRESSION) {
  // code1
} 
else {
  // code2
}
```

* If the BOOLEAN_EXPRESSION evaluates to true, then code1 block is executed. Otherwise code2 block is executed.
* Example

```c++
int x = 4;
if ((x > 3) && (x < 6)) {
  cout << "x is either 4 or 5" << endl;
} 
else {
  cout << "x is not 4 or 5" << endl;
}
```

* Notice the curly braces, i.e. "{ ... }", also known as block statements. 
  * This allows many statements to be executed.
  * Without "{ ... }", only the following statement will be considered as part of that condition's block, and other statements are considered outside the block statement.
  * Example

```c++
int x = 4;
if ((x > 3) && (x < 6))
  cout << "x is either 4 or 5" << endl;
else
  cout << "x is not 4 or 5" << endl;
// Will have the same output as the last statement.

int x = 6;
if ((x > 3) && (x < 6))
  cout << "1" << endl;
  cout << "2" << endl; // outside if block
  cout << "3" << endl; // outside if block
```
  
  * The last two statements will always execute because they are considered outside of the code block.
  * A syntax error will appear if you try to insert an `else` after the statements since `else` can only be used after an `if` code block.
  * Note that the syntax is **NOT** `elif`, like it is in Python; you need to write out `else if() {...}`

# Multi-way If-else Statements

* Programs may require more than simply two paths of code execution.
* Multiple if-else statements can allow the program to execute many branches.
* In a multiway if/else structure, the compiler looks through each block to see if the condition evaluates to true; if it does, the rest of the structure is ignored
* If none of the conditions evaluate to true, the contents of the `else` block are executed

* Example

```c++
int x = 3;
if (x == 1)
  cout << "x equals 1" << endl;
else if (x == 2)
  cout << "x equals 2" << endl;
else if (x == 3)
  cout << "x equals 3" << endl;
else
  cout << "x does not equal 1, 2, or 3" << endl;
```

Remember to surround all code blocks with braces! We prefer that you write the above code block as shown below. This way, if you ever need to add another line of code to a block, you won't have to remember to add the curly braces, they will already be there.

```c++
int x = 3;
if (x == 1) {
  cout << "x equals 1" << endl;
}
else if (x == 2) {
  cout << "x equals 2" << endl;
 }
else if (x == 3) {
  cout << "x equals 3" << endl;
}
else {
  cout << "x does not equal 1, 2, or 3" << endl;
}
```

# Vim navigation trick

Having to alternate between vim and Unix by repeatedly typing `:q` and `vim [filename]` can sometimes get tedious.
You can temporarily push Vim to the background so that you can use the command line.

To do so, make sure that you are in the "Command mode" for Vim.

Pressing Ctrl key followed by z (usually written in instructions as Ctrl+z) will put the Vim window in the background, giving you back the command-line prompt.

Type `fg` and press Enter, to get back into Vim (`fg` stands for "**f**ore**g**round").

`w` and `v` in Vim will jump the cursor from the next and previous word, respectively, while in "Command mode".

# Shortcut of the day

`ll` can be the same as `ls -l`, if you type `alias ll='ls -l'` on the command line (it will be remembered until you close that session).

Personally, I use `alias ll='ls -lFG'`.


# Reminder
Remember to practice syntax (include semicolons, pound signs, etc.).
Observing in-class code is not sufficient, review the lab and textbook examples to practice programming and better prepare for quizzes and tests.
When writing programs, try refine them to be more efficient (eliminate repetitive code when possible).

# Practice Questions
1. What is the following output of this code snippet? Assume it's implemented in a working C++ program.
```
int x;
cout << x << endl;
```
2. What is the following output of this code snippet? Assume it's implemented in a working C++ program.
```
double y = 1.2;
int x = 3.5 + 2.4 + y;
y += x;
cout << x << endl;
cout << y << endl;
```
3. Exclusive-or (xor) is defined as the following on two boolean values:
```
xor returns true if only one of the boolean values are true; which means, xor returns false if both the boolean values are false or both the boolean values are true
```
Represent xor by using a combination of only !, &&, ||
