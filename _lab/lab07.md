---
layout: lab
num: lab07
ready: true
desc: "Linked lists"
assigned: 2019-05-22 08:00:00.00-8
due: 2019-05-31 23:59:00.00-8
---

# Goals of this lab

The goal of this lab is get more practice with iterating through linked lists and solving problems. Continue to practice code tracing to reason about your code. 

### Step by Step Instructions: PLEASE READ CAREFULLY!

## Step 1: Getting Started

Please refer to previous labs for additional instructions on creating a github repo for this lab.

## Step 2: Obtaining the starter code

* Navigate to your cs16 directory and clone the git repository you created
```
git clone git@github.com:ucsb-cs16-w19/lab07_jgaucho.git
```
* cd into this new directory
```
cd lab07_jgaucho
```

* Copy the starter code by typing the following command:

```
cp /cs/faculty/ykk/cs16/labs/lab07/* ./
```

Typing the list (`ls`) command should show you the following files in your current directory

```
$ ls
linkedListFuncs.cpp  Makefile                 tddFuncs.cpp
linkedListFuncs.h    moreLinkedListFuncs.cpp  tddFuncs.h
linkedList.h         moreLinkedListFuncs.h
llTests.cpp          README.md
$
```


## Step 3: Reviewi the files and your tasks

Here is a list of your tasks for this lab:

### Step 3a: Familiarize yourself with the big picture

Type `make tests` and you will see some tests pass, but some fail.

You are finished when all the tests pass. We have implemented a few functions that involve linked lists in `linkedListFuncs.cpp`. There is only one file you need to edit this week:

<code>moreLinkedListFuncs.cpp</code> contains more functions that deal with linked lists.  

### Step 3b: Add the file header

Include the following header block at the top of your <code>moreLinkedListFuncs.cpp</code> file and make sure to update it accordingly:

```
/*=============================================================================
 |   Assignment:  ASSIGNMENT NUMBER AND TITLE
 |
 |       Author:  STUDENT'S NAME HERE
 |
 |   To Compile:  EXPLAIN HOW TO COMPILE THIS PROGRAM
 |
 |        Class:  NAME AND QUARTER OF THE CLASS FOR WHICH THIS PROGRAM WAS
 |                      WRITTEN
 |     Due Date:  DATE AND TIME THAT THIS PROGRAM IS/WAS DUE TO BE SUBMITTED
 |
 +-----------------------------------------------------------------------------
 |
 |  Description:  DESCRIBE THE PROBLEM THAT THIS PROGRAM WAS WRITTEN TO SOLVE.
 |
 |        Input:  DESCRIBE THE INPUT THAT THE PROGRAM REQUIRES.
 |
 |       Output:  DESCRIBE THE OUTPUT THAT THE PROGRAM PRODUCES.
 |
 |    Algorithm:  OUTLINE THE APPROACH USED BY THE PROGRAM TO SOLVE THE
 |      PROBLEM.
 |
 |   Known Bugs:  IF THE PROGRAM DOES NOT FUNCTION CORRECTLY IN SOME
 |      SITUATIONS, DESCRIBE THE SITUATIONS AND PROBLEMS HERE.
 |
 *===========================================================================*/

```

### Step 3c: Work on the linked list functions

Working on the linked list functions below is one of the most important things you can do to prepare for the final exam.

There are 7 functions you will need to write for this lab:

* <code>addIntToEndOfList</code>
* <code>addIntToStartOfList</code>
* <code>pointerToMax</code>
* <code>pointerToMin</code>
* <code>largestValue</code>
* <code>smallestValue</code>
* <code>sum</code>


Each one has a set of tests which can be found under its corresponding heading when you type <code>make tests</code>. For example, the `addIntToEndOfList` tests look like this to start: 

```
./llTests 1
--------------ADD_INT_TO_END_OF_LIST--------------
PASSED: linkedListToString(list)
   FAILED: linkedListToString(list)
     Expected: [42]->[57]->[61]->[12]->null Actual: [42]->[57]->[61]->null
   FAILED: linkedListToString(list)
     Expected: [42]->[57]->[61]->[12]->[-17]->null Actual: [42]->[57]->[61]->null
PASSED: linkedListToString(empty)
   FAILED: linkedListToString(empty)
     Expected: [0]->null Actual: null
   FAILED: linkedListToString(empty)
     Expected: [0]->[19]->null Actual: null

```

You should replace each function stub with the correct code for the function until all of the tests for each one pass. It is recommended that you work on the functions one at a time in the order that they are presented above. That is, get all the tests to pass for `addIntToStartOfList` then `addIntToEndOfList` and so on. When all the tests pass, move on to the next step. 

## Step 4: Checking your work before submitting

When you are finished, you should be able to type  <code>make clean</code> and then <code>make tests</code> and see the following output:


```
-bash-4.2$ make clean
/bin/rm -f llTests *.o
-bash-4.2$ make tests
g++ -Wall -Wno-uninitialized   -c -o llTests.o llTests.cpp
g++ -Wall -Wno-uninitialized   -c -o linkedListFuncs.o linkedListFuncs.cpp
g++ -Wall -Wno-uninitialized   -c -o moreLinkedListFuncs.o moreLinkedListFuncs.cpp
g++ -Wall -Wno-uninitialized   -c -o tddFuncs.o tddFuncs.cpp
g++ -Wall -Wno-uninitialized  llTests.o linkedListFuncs.o moreLinkedListFuncs.o tddFuncs.o -o llTests
./llTests 1
--------------ADD_INT_TO_END_OF_LIST--------------
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
./llTests 2
--------------ADD_INT_TO_START_OF_LIST--------------
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
./llTests 3
--------------POINTER_TO_MAX--------------
PASSED: pointerToMax(list1)
PASSED: pointerToMax(list1)
PASSED: pointerToMax(list1)->data
PASSED: pointerToMax(list1)->next->data
PASSED: pointerToMax(list2)
PASSED: pointerToMax(list2)
PASSED: pointerToMax(list2)->data
PASSED: pointerToMax(list3)
PASSED: pointerToMax(list3)
PASSED: pointerToMax(list3)->data
PASSED: pointerToMax(list4)
PASSED: pointerToMax(list4)
PASSED: pointerToMax(list4)->data
PASSED: pointerToMax(list4)->next->data
./llTests 4
--------------POINTER_TO_MIN--------------
PASSED: pointerToMin(list1)
PASSED: pointerToMin(list1)
PASSED: pointerToMin(list1)->data
PASSED: pointerToMin(list1)->next->data
PASSED: pointerToMin(list2)
PASSED: pointerToMin(list2)
PASSED: pointerToMin(list2)->data
PASSED: pointerToMin(list3)
PASSED: pointerToMin(list3)
PASSED: pointerToMin(list3)->data
PASSED: pointerToMin(list4)
PASSED: pointerToMin(list4)
PASSED: pointerToMin(list4)->data
PASSED: pointerToMin(list4)->next->data
./llTests 5
--------------LARGEST_VALUE--------------
PASSED: largestValue(list1)
PASSED: largestValue(list2)
PASSED: largestValue(list3)
PASSED: largestValue(list4)
./llTests 6
--------------SMALLEST_VALUE--------------
PASSED: smallestValue(list1)
PASSED: smallestValue(list2)
PASSED: smallestValue(list3)
PASSED: smallestValue(list4)
./llTests 7
--------------SUM--------------
PASSED: sum(list1)
PASSED: sum(list2)
PASSED: sum(list3)
PASSED: sum(list4)

-bash-4.2$
```

At that point, you are ready to try submitting on gradescope.


## Step 5: Submitting via gradescope

Submit the `moreLinkedListFuncs.cpp` file on gradescope.

# Grading Rubric

Most of the points will be awarded based on gradescope automatic grading. Other points will be assigned after visual code inspection by TAs/graders.

## Gradescope automatic points

<table border="1">
<tr><th>Test Name</th><th>Value</th></tr>
<tr><td><p style="color:green;margin:0;padding:0;">addIntToEndOfList</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">addIntToStartOfList</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">pointerToMax</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">pointerToMin</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">largestValue</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">smallestValue</p></td><td>(10 pts)</td></tr>
<tr><td><p style="color:green;margin:0;padding:0;">sum</p></td><td>(10 pts)</td></tr>
</table>

## Code inspection human-assigned points

* (10 pts) Code style, including but not limited to:
1. Code can be easily understood by humans familiar with C++ (including both the author(s) of the code, and non-authors of the code.)
2. Code is neatly indented and formatted, following standard code indentation practices for C++ as illustrated in either the textbook, or example code given in lectures and labs
3. Variable names choices are reasonable
4. Code is reasonably "DRY" (as in "don't repeat yourself")&mdash;where appropriate, common code is factored out into functions
5. Code is not unnecessarily or unreasonably complex when a simpler solution is available

## An important word about academic honesty and the gradescope system

We will test your code against other data files too&mdash;not just these.  So while you might be able to pass the tests on gradescope now by just doing a hard-coded output, that will NOT receive credit.    

To be very clear, code like this will pass on gradescope, BUT REPRESENTS A FORM OF ACADEMIC DISHONESTY since it is an attempt to just "game the system", i.e. to get the tests to pass without really solving the problem. Submitting a program of this kind would be subject not only to a reduced grade, but to possible disciplinary penalties.    If there is <em>any</em> doubt about this fact, please ask your TA and/or your instructor for clarification.
