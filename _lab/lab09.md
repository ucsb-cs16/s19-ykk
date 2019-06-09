---
layout: lab
num: lab09
ready: true
desc: "Putting What You Learned into Practice"
assigned: 2019-06-05 08:00:00.00-7
due: 2019-06-13 23:00:00.00-7
---

# Goals for this lab

By the time you have completed this lab, you should be able to

* Use a text-editor to create and edit C++ programs
* Use if/else and for loops
* Create header files and write the corresponding function definitions
* Write helper functions to create reusable pieces of code
* Show that you understand how to work through the basic process of test-driven development in C++
* Write a Makefile to compile and run your code
* Integrate github into your work flow

This lab has no starter code. The goal is for you to use what you have learned throughout the course to design and implement a solution to a given problem. Feel free to discuss your approaches with the tutors and the instructor.

The exercises below are based on the programming projects listed in the book. For this lab, choose one of the programming projects below and implement it using the test-driven approach that we have used this quarter (e.g., create a header and the cpp file together with the test program that uses `assert`s; include a Makefile that runs all tests).


## Step 0: Find your partner

* You can work alone or with a partner who should be in your section. If you are working with a partner, you should follow the pair-programming guidelines: <https://ucsb-cs16.github.io/topics/pair-programming/>.

* Choose who will be the pilot/driver for the first part of the lab. The pilot should sit down in front of the computer now. The navigator gets a chair and sits next to the pilot. You should exchange roles after awhile, before the pilot gets tired, and before the navigator gets bored or distracted.


## Step 1: Create a new repo, add your partner as collaborator on GitHub and Gradescope

* Create a repo for this lab on the pilot's github account. 
    * Log into the pilot's github account. From the drop down menu on the left, **select our class organization** and proceed to create a new repo. 
    * **Follow this naming convention**: If your github username is `jgaucho` and your partner's is `alily`, you should name your repo `lab09_agaucho_alily` (usernames appear in alphabetical order). 
    * You must set the visibity of your repo to be 'PRIVATE' when creating it.
    * Remember to add the C++ `.ignore` option from the drop down menu. 
    * Include a `README` file.

* The pilot should add the navigator as a collaborator on github. To do this navigate to the git repo you just created. Choose the "Settings" tab. Then click on the 'Collaborators and teams' option on the left. Scroll all the way down and add the navigator's github account. Then press on the 'Add collaborator' button. Now you and the navigator share the ownership of your git repo.

* *To submit your code, also make sure to **add your partner on Gradescope**.* Add them now, before you forget. 



## Step 2a: Clone the repo in the pilot's account and update the README

* Using the web-browser, navigate to your newly created repo on github. Find the address of your git repo. Click on the green "clone or download button", and select the "Use SSH" option. 

* Clone your repo into your csil account by typing `git clone git@github.com:ucsb-cs16-XXX.git` on the terminal, **replacing `XXX` in the last argument** with the address of your git repo.

* Open the `README.md` file that should be in your repo (if you didn't select that option when creating the repo, you can create it).

* Add the following information to your repo, updating it with the following info

```
     |   Assignment:  ASSIGNMENT NUMBER AND TITLE
     |
     |       Author:  STUDENT1 and STUDENT2 NAME(s) HERE
     |
     |        Class:  NAME AND QUARTER OF THE CLASS FOR WHICH THIS CODE WAS WRITTEN
     |                      
     |      Program:  THE NAME OF THE PROGRAM THAT YOU CHOSE TO IMPLEMENT
     |
     |   To Compile:  EXPLAIN HOW TO COMPILE THIS PROGRAM
     |
```

## Step 2b: Commit the repo

**Make sure that before the lab is over, you commit your README** with the updated information.

```
git add .
git commit -m "Initial version of lab09 README"
git push origin master
```



# Step 3: Select a project and create the necessary files

* You must follow a TDD style of coding. Write your own test code in a separate file called **projectXTest.cpp**, **replacing `X` with the number of the project** that you selected.

 * Write a Makefile to compile the code. Use the example structure in previous labs as your template. Read the [following instructions about Makefiles](https://ucsb-cs16.github.io/topics/makefile/) and the [make process](https://ucsb-cs16.github.io/topics/make/).


<br/>
<br/>
<br/>

It's time to select and implement your project!


-----

# Project 1: Race results

In many races competitors wear an RFID tag on their shoe or bib. When the racer crosses a sensor a computer logs the racer's number along with the current time. Sensors can be placed along the course to accurately calculate the racer's finish time or pace and also to verify that the racer crossed key checkpoints. Consider such a system in use for a half marathon running race, which is 13.1 miles. In this problem there are only three sensors: at the start, at the 7 mile point, and at the finish line.

Below is sample data for three racers. 
* The first line is a timestamp of when the the race began.
* The other lines in the file are in the format `<sensor>,<racer number>,<timestamp>` where
   * `<sensor>` is the ID of the sensor that recorded the data  (`0=start, 1=midpoint, 2=finish`),
   * `<racer number>` is the ID of the racer, and 
   * `<timestamp>` is the timestamp of when the racer was detected by the sensor. (Note that a racer's start time may be different than the real start time because sometimes it takes a racer a little while to get to the starting line when there is a large pack.)

All timestamps are in the 24 hour time format (`HH MM SS`). 

    08 00 00
    0,100,08 00 00
    0,132,08 00 03
    0,182,08 00 15
    1,100,08 50 46
    1,182,08 51 15
    1,132,08 51 18
    2,132,09 34 16
    2,100,09 35 10
    2,182,09 45 15

Create a text file with a sample race log called `"race.log"`. Write a program that reads the log data from a file into array(s) or vector(s). The program should then call functions, which given a racer's number output the racer's overall finish place, race split times in minutes/mile for each split (i.e. the time between sensors), and the overall race time and overall race pace.

-----

# Project 2: Encryption

You and your friends decided to use a secret code to communicate with each other.
You implemented a basic encryption method based on the ASCII code. (Appendix 3 in the book shows the ASCII character set.) Individual characters in a string are encoded using this system. For example, the letter "A" is encoded using the number 65 and "B" is encoded using the number 66.

Your secret code takes each letter of the message and encrypts it as follows:
```c++
if (OriginalChar + Key > 126) then
    EncryptedChar = 32 + ((OriginalChar + Key) – 127)
else
    EncryptedChar = (OriginalChar + Key)
```

For example, if the Key = 10 then the message "Hey" would be encrypted as:

    Encrypted H = (72 + 10) = 82 = R in ASCII
    Encrypted e = (101 + 10) = 111 = o in ASCII
    Encrypted y = 32 + ((121 + 10) – 127) = 36 = $ in ASCII

Consequently, "Hey" would be transmitted as "Ro$."

Write a program that decrypts the encrypted message. You might want to create a function, which will take an encoded string and a key as an input and return the decoded string. You might want a separate function that checks whether the decoded string is valid.

The ASCII codes for the unencrypted message are limited to the visible ASCII characters. For simplicity, assume that the key is a number between 1 and 100. Your program should try to decode the message using all possible keys between 1 and 100. When you try the valid key, the message will make sense. For all other keys, the message will appear as gibberish.

In order to not have to look at the output of the 100 attempts, to assess whether the decoded message makes sense, you can check that the resulting output string contains a "keyword": i.e., a word that you include in your message, specifically for this check (this is, for instance, how Alan Turing was able to [crack the Enigma code](https://www.iwm.org.uk/history/how-alan-turing-cracked-the-enigma-code)). For example, if your keyword is "Hey", then you know whether you encoded a given string "Ro$" correctly, if "Hey" appears in the resulting string.


-----

# Project 3: Time conversion

Write a function that takes a string parameter containing the time. This function should convert the time into a four-digit military time based on a 24-hour clock. For example,"`1:10 AM`" would output "`0110 hours`", "`11:30 PM`" would output "`2330 hours`", and "`12:15 AM`" would output "`0015 hours`". Adding a period inside AM or PM (e.g., "`9 A.M.`") should also be accepted.
The function should return the resulting time as a string. Be sure to not include any whitespace in the resulting string.

**Update**: Since the instructions specify that there shouldn't be any whitespace in the resulting string **do not include ` hours`** in the resulting string. Also, "`9:30 A.M.`" and "`09:30 A.M.`" should result in the same output (what other equivalences would you need?).

-----


## Step 4: Submit

Push all your code to github. Then submit your repo on gradescope.


## Step 5: Done!
Remember to check your code for appropriate comments, formatting, tests.

If you are in the Phelps lab or in CSIL, make sure to log out of the machine before you leave. Also, make sure to close all open programs before you log out. Some programs will not work next time if they are not closed. Remember to save all your open files before you close your text editor.

If you are logged in remotely, you can log out using the exit command:

`$ exit`







# Evaluation and Grading <a name="eval"></a>

* Setup and style (15 pts)

    * (5 pts) Correct creation of the lab github repo _in our class organization_ following the naming conventions provided in the lab. Adding your partner as collaborator and partner accepting the invitation. Both partners joining the same group on gradescope.

    * (5 pts) The repo contains a correctly updated `README.md`

    * (5 pts) All files have good programming style, including proper use of indentation, reasonable choices for variable names, readable code, reasonable use of whitespace, and other good programming practices. You must use curly braces in the body of all control structures (if-else, for and while) even if they contain a single statement. You should not mix tabs and spaces when indenting your code. *The first line of every file should be the name of your file, followed by date of creation, author and a brief description of the program.*

* Code (100 pts)

    * The repo included the necessary .h, .cpp, **projectXTest.cpp** and the input files (if applicable). 
    * The Makefile successfully executes `make tests` and displays the results.


