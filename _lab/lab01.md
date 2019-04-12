---
layout: lab
num: lab01
ready: true
desc: "Crunching numbers: Loops and functions "
assigned: 2019-04-09 8:00:00.00-7
due: 2019-04-16 23:59:00.00-7
---

<div markdown="1">

## Goals for this lab

In this lab you will get practice 
* using github's web interface
* using `for` loops and `while` loops
* calculating a series using `for` loops and `if-else` statements
* working with other data types (`doubles`)
* writing nested loops
* writing functions


These exercises are inspired by the ones from the textbook (in Ch. 2 and Ch. 3) - but they are NOT the same, so follow the instructions on THIS page carefully.


**You are not expected to finish the entire lab in one sitting. Please don't rush through it and read all instructions carefully.**

## Logging on to CSIL

Follow the instructions on this page to log yourself into CSIL through your COE account.

<https://ucsb-cs16.github.io/topics/ssh_connect/>

There's a better alternative to Putty for Windows users, by using Git. The instructions are on Piazza through this link, go to option 2.

<https://piazza.com/class/ju19d0pmd093r8?cid=9>

## Log in and create a local directory

* Log into your CoE account on CSIL and open a terminal.
* Under your **cs16** directory, you should create a new directory named **{{page.num}}** (refer to lab00 for instructions if you have forgotten how to do this)

You are now ready to get the starter code.

## Getting the starter code  <a name="getstarter"></a>

The following instructions will work only if you are working on the CSIL server. If you are working on your laptop, you will need to use remote copy via `scp`.
<https://ucsb-cs16.github.io/topics/csil_copying_files/>

Copy the code from the instructor's account _on the CSIL server_ into your **{{page.num}}** directory _on the CSIL server_ by issuing the following command (**remember that `-bash-4.2$` represents the command prompt and you don't need to type it in**):

```
-bash-4.2$ cp /cs/faculty/ykk/cs16/labs/{{page.num}}/* ~/cs16/{{page.num}}/
```
After running this command, if you `cd` into **~/cs16/{{page.num}}/** and use the `ls` command, you should see three **.cpp** files and a README:

```
-bash-4.2$ ls
min2.cpp  min3v1.cpp  min3v2.cpp README.md
-bash-4.2$
```

If you don't see those files, go back through the instructions and make sure you didn't miss a step. If you still have trouble, ask your TA or tutor for assistance.


# # # # # # # Skip the Following Step for creating a repo # # # # # # 

## Create a repo on github in our class organization

For this lab and all subsequent programming assignments, you should start by creating a repo _in the **[{{ site.github_org_name }}]({{ site.github_org_url }})** organization_. 
**You may not receive any credit for this lab if you do not create the repository under the organization (i.e., do NOT create it in your own account).**

Make sure that when you create a repo, the **Owner** is the **{{ site.github_org_name }}** organization (**NOT** your personal account).

**IMPORTANT**. 
If you haven't completed the **"Setup GitHub and add yourself to our organization" steps from Lab00**, then make sure you do it now, otherwise, you won't be able to access the organization and follow the steps below. 

When you verified that your GitHub account is associated with the correct email address (see Lab00 instructions), you can follow these steps to create a new repo:

* Navigate to your dashboard on [https://github.com/](https://github.com/). From the left drop down menu, select the class organization.
* Click on the green "New repository" button to create a new repository.

* Type the name of your repo following the naming convention **`{{page.num}}_your-github-username`**. For example if your github username is _jgaucho_, you should name your repo as **`{{page.num}}_jgaucho`**. 

* Select the "Private" visibility option so that other students in the org cannot view your code.

* Add the C++ **.ignore** option from the dropdown menu and click on "Create repository" button. 


## Upload the initial version of your code using github's web interface 

* Upload the files in your {{page.num}} directory to the new repo you created in the previous step. To do this, **you should be physically present on a lab machine or in CSIL** where you have access to **a web browser and a local copy** of your files (min2.cpp  min3v1.cpp  min3v2.cpp README.md). 
    * On your web browser, navigate to your repo on github. 
    * Click on the "Upload files" button.

* Now either drag and drop the files: from your machine or use the "Choose your files" option to browse through your local directory and upload the file. Then press the green "Commit new files" button. Navigate back to your repo to see that the files you uploaded are correctly listed. Click on it and you should see your code on github's web interface. 

You have created an initial copy of the starter files for this lab.

_Alternatively_ (i.e., instead of using the web interface), you can commit your files using `git` commands on the command line. Ask the instructor or the mentors if you get stuck.


# Solving the problems for this lab<a name="programs"></a>

This assignment consists of 3 problems, each of which is described below. The first one is worth 20 points each, and the last two are worth 40 points each. 

Each problem should be solved **in its own file** and **all three** must be submitted for full assignment credit. **The autograder tests will NOT pass if all files are not submitted.**


You will need to create three files named `block.cpp, min4.cpp, and pi.cpp`:
Each corresponds to one of the problems listed below, which make up this lab.

For a reminder on how to open and use a text editor to create and edit new source files, refer back to Lab 00.

For all the subproblems given in this assignment you must compile your code frequently (as you develop it), and test it extensively with as many inputs as you can think of.

<hr>

### Print a block

* Navigate to your **{{page.num}}** directory using the `cd` command.
* open a file called **block.cpp** using the same editor you used for the previous labs.
* In that file, write a program that takes an input from a user for the number of rows and number of columns and prints out a block of characters that is based on these 2 parameters. The program should keep asking the user for input, and printing out the result, until the user enters zero for **either** of the input parameters.

A session should look <b><i>exactly</i></b> like the following example for all the different inputs and the output (**including whitespace and formatting** - note that there is **NO whitespace at the end of each of these lines**):

```
$ ./block
Enter number of rows and columns:
1 5
X.X.X.X.X.
Enter number of rows and columns:
2 2
X.X.
X.X.
Enter number of rows and columns:
2 5
X.X.X.X.X.
X.X.X.X.X.
Enter number of rows and columns:
10 5
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
X.X.X.X.X.
Enter number of rows and columns:
0 1
```

Note that when you are collecting user input, if you want to store the values in two variables, e.g., `var1` and `var2`, then the `cin` statement would be as follows (no need to provide a space between the two variables inside your code):

```c++
cin >> var1 >> var2;
```


Each string printed by the program should include a newline at the end, but **NO other trailing whitespace** (i.e., **do NOT include extra space** characters at the end of the line). **Make sure that you have no typos in your code!** The autograder tests will not pass if your solution does not match _exactly_ (not just _look_ exactly the same).

For this problem you have to use a `for` loop, a `while` or `do-while` loop. While loops are similar in that the code inside the body of the while is repeated as long as the while condition is true. Here is the syntax for `while`

```cpp
while('expression'){
	//Repeat these statements
}
```

`'expression'` should be replaced by the appropriate boolean expression. The body of the loop is executed as long as the expression is true. E.g.,

```cpp
int x = 5;
while (x > 0){
    cout << x << " ";
	x--;
}
```
The above code prints "5 4 3 2 1 " (_includes_ a space at the end).

You can achieve a simiar behavior by using a `for` loop.
The `while` and `for` loops can be interchanged, but some loop formats are more convenient than others in different situations.

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





To compile your code use the `g++` command:

`$ g++ -std=c++11 -o block block.cpp`


Note that the `-std=c++11` flag is optional to use (that is, not critical to define). All this does is force the compiler to use the latest version of C++.


<b>If you encounter an error, use the compiler hints and examine the line in question. If the compiler messsage is not sufficient to identify the error, you can search online to see when the error occurs in general.</b>

Run your executable as follows to test it out.
`$ ./block`

	Remember to re-compile the relevant files after you make any changes to the C++ code.

Upload your files to your repo on github using github's web interface following the instructions at the beginning of this lab.


<hr>


### Calculate the approximate value of PI

Write a C++ program in a file named **pi.cpp** that approximates the value of the constant π. Once again you should not resort to using predefind constants and functions for π, that are provided by C++ standard libraries. Instead you should compute the value of π based on the Leibniz formula for π. The formula is given below:

```
 1 – 1/3 + 1/5 – 1/7 + 1/9 ...  = pi/4
```

Put another way, the formula can be written as:

```
pi = 4 · [ 1 – 1/3 + 1/5 – 1/7 + 1/9 ... + (–1 ^ n)/(2n + 1) ]
```

The Leibniz formula works well for high values of n.

Here is a link that gives the approximated values of pi for up to 1000 terms: <http://www.eveandersson.com/pi/gregory-leibniz>


The program takes an input from the user for the value of n, which determines the number of terms in the approximation of the value of pi (i.e., **the approximation is using n + 1 terms**). The program then outputs the approximated value of pi as calculated by the Leibniz formula. You must also include a loop that allows the user to repeat this calculation for new values of 'n' until the user says she or he wants to end the program by issuing an input of -1 (or any other negative number). You may assume that the user always inputs an integer.

The program should print a string of text to the terminal before getting each piece of input from the user. A session should look like the following example (**including whitespace and formatting**), showing the expected output for different inputs:

```
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
0
The approximate value of pi using 1 term is: 4.000
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
3
The approximate value of pi using 4 terms is: 2.895
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
9
The approximate value of pi using 10 terms is: 3.042
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
49
The approximate value of pi using 50 terms is: 3.122
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
99
The approximate value of pi using 100 terms is: 3.132
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
999
The approximate value of pi using 1000 terms is: 3.141
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
9999
The approximate value of pi using 10000 terms is: 3.141
Enter the value of the parameter 'n' in the Leibniz formula (or -1 to quit):
-1
```
Be sure to **have a newline after each "Enter the value..." prompt and no other white spaces.**

Each string printed by the program should include a newline at the end, but **NO other trailing whitespace** (i.e., **do NOT include extra space** characters at the end of the line). **Make sure that you have no typos in your code!** The autograder tests will not pass if your solution does not match _exactly_ (not just _look_ exactly the same).

In addition, all approximated floating pointer numbers must be displayed to **exactly three digits after the decimal point**. To do this you should use set the precision for displaying floating point numbers before any of the `cout` statements in your code. This is done by including the following lines **inside of your `main()`**:

```
cout.setf(ios::fixed); 	   // Display in fixed point notation. For example, display 1e-1 as 0.1
cout.setf(ios::showpoint); // Always display the decimal point.
cout.precision(3);         // Set the number of digits to display after the decimal point to 3
```
To calculate x to the power of y, use the `pow(x,y)` function from the standard library. To do this you will need to `#include` the header file: `cmath`

<hr>

Upload your files to your repo on github using github's web interface. (You will need to be on a csil machine and not remotely logged in to do this step (because you need to use a web browser with access to those files). Disregard this if you're working on your own machine.

### Calculate the minimum of 4 numbers

In this part of the lab you will write a program that compares 4 input numbers and prints out the smallest one.

**You should not use the *min()* function in C++ algorithm library or any other outside function that performs the minimum operation for you. Instead, you should base the program on the example programs provided to you that compare fewer inputs.**


Start by examining the given examples, also described below:

<b>min2.cpp</b>

This program takes two command-line arguments, and converts them to integers.  It then calls a function, `smallest_of_two`, that returns the smallest of the two numbers (or the value they share in case of a tie.) It then prints out the result of that function call.

<b>min3v1.cpp</b>

This is the first of two versions of a program that takes **min2.cpp** one step further, finding the smallest value from among three numbers. Again, if there is a tie, it prints the tie value. Look at the nested if/else statements and see if you can make sense of the logic. Seek help if you don't.

<b>min3v2.cpp</b>

This program does EXACTLY the same thing as **min3v1.cpp**, but does it with much cleaner, simpler code. Notice how we REUSE the `smallest_of_two` function to build up a `smallest_of_three` function.

Your job in this step is to test min2, min3v1 and min3v2 with many different values and convince yourself that they work properly.

In the next step, you will be taking these programs to the next logical step in this sequence.

<b><i>Your main task</i></b>: Write min4.cpp

* Write a program that works just like min2 and min3v1 and min3v2, except it takes four ints on the command line, and prints the smallest value, handling ties appropriately.

* We encourage you to follow the model of min3v2.cpp if you can understand how this works, since your code will be far cleaner than trying to build this out of nested if/else statements.

If you DO use nested if/else statements, though, be sure that you indent and format your code appropriately.

Follow the pattern in min2 and min3v1/min3v2 in terms of all other issues and how they are handled, including the usage message, etc. Your program should look exactly like these except that it works on 4 inputs (note, there are no trailing whitespacse):

```
./min4
Usage: ./min4 num1 num2 num3 num4
 Prints smallest of the four numbers
```
Here is the output of the program with the correct number of inputs:

```
$ ./min4 3 4 5 6
3
```
Here are two more example runs:

```
$ ./min4 92 35 12 17
12

$ ./min4 92 -35 12 17
-35

```


To compile your code use the g++ command as before.

`$ g++ -std=c++11 -o min4 min4.cpp`

Run your executable with different inputs to test it out.

Upload your files to your repo on github using github's web interface.



## Submit your code on Gradescope<a name="submit"></a>

Once you are satisfied that **your programs are correct**, then it's time to submit them. Note that Gradescope will display an error if you don’t upload **all six files**.


Log into your account on [https://www.gradescope.com/](https://www.gradescope.com/) and navigate to our course site. Select this assignment. Then click on the "Submit" button on the bottom right corner to make a submission. 

You should receive full credit for a completely correct program that follows the style conventions described below.








## Log Out!<a name="done"></a>

You are now done with this assignment!
If you are in the Phelps lab or in CSIL, make sure to log out of the machine before you leave. Also, make sure to close all open programs before you log out. Some programs will not work next time if they are not closed. Remember to save all your open files before you close your text editor.

If you are logged in remotely, you can log out using the `exit` command:

`$ exit`


## Grading rubric

In addition to the points given by gradescope, our staff may be manually grading your code for style. Code style, includes but is not limited to the following:

1. Code can be easily understood by humans familiar with C++ (including both, the author(s) and non-authors of the code.)
2. Code is neatly indented and formatted, following standard code indentation practices for C++ as illustrated in either the textbook, or example code given in lectures and labs
3. Variable names choices are reasonable
4. Code is reasonably "DRY" (as in "don't repeat yourself")&mdash;where appropriate, common code is factored out into functions
5. Code is not unnecessarily or unreasonably complex when a simpler solution is available

# Github Resources
* [Overview of git](https://ucsb-cs56-pconrad.github.io/topics/git_overview/)

* [Creating a github repo under an organization](https://ucsb-cs16.github.io/topics/github_com_create_private_repo_under_org/).

* [About gitignore](https://ucsb-cs56-pconrad.github.io/topics/git_gitignore/)



</div>

