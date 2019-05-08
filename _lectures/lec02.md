---
num: "lect02"
desc: "Hello World! + unix, vim"
ready: true
reading: Chapter 1, Section 1.1 and 1.3
pdfurl: https://drive.google.com/open?id=1zP7YNmZXCYnAP8MrEiaf1Ov28ESpXR0s
lecture_date: 2019-04-04
---


# Topics
* Programming in the unix environment
* The vim (editor) survival skills (to avoid this: <https://www.commitstrip.com/en/2017/05/29/trapped> :-))
* Writing, compiling and running a C++ program ("hello world") program
* Breaking down the hello world program

# Programming in the unix environment
* Unix is an operating system just like Windows and Mac OS
* All your data and programs are stored in files, within the unix filesystem
* File vs. directory
* Files are organized within the *unix filesystem*
* You can navigate the filesystem with some simple commands inside a terminal:
	- ls
	- mv
	- cp
	- pwd
	- mkdir
	- cd
* Relative path vs. absolute path (important for mv, cp, mkdir, cd)
* There are also some shortcuts to typing in the terminal
	- `Ctrl + a` moves the cursor to the start of the line
	- `Ctrl + e` moves the cursor to the end of the line
	- `Ctrl + z` while in an application, suspends the app, puts it in the background, and exits back to the terminal (type `fg` on the command line to bring it back)
	- `Ctrl + c` similar to `Ctrl + z`, but aborts an application instead

# Basic Unix Commands

In the displayed commands, don't include brackets. E.g., `mkdir [name]` will look like `mkdir tmp`, if you want to create a directory called `tmp`.


`pwd`
**p**rint (the) **w**orking **d**irectory - displays the full (absolute) path to the directory you are currently in

User's **home directory** has a shortcut/alias denoted by a tilde symbol: `~`
* a home directory is **relative** to the user that's logged in
* the _absolute_ that is aliased by `~` depends on the user

`~`
refers to the home directory

`.`
refers to the current directory

`..`
refers to the directory one level above the current one


`ls [dir]` lists the contents of a directory `dir` 
* if no directory is specified, it will list the contents of the current directory (denoted by `.`)
* if no directory is specified, it is equivalent to `ls .`

`ls -l` 
lists the contents of a directory, and provides additional information about the file/directory; 
distinguishes between files and directories (if the line starts with the letter ‘d’, then it corresponds to a directory, if not, then it corresponds to a file)

`mv [src] [dest]` 
move a **file/directory** called `src` to a file/directory called `dest` (if you are moving a file (file1) to another filename (file2), then you are effectively renaming file1)

`mv [src1] [src2] [dest]` 
move the specified files to a directory called `dest` 

`rm [file]`
deletes/removes a file (use with caution because it deletes files irrecoverably)

`rm -r [dir]`
recursively deletes the contents of a directory ; 
if you use only `rm` for a directory, the operating system will complain and display the error message: `cannot remove [dir]: Is a directory`

`mkdir [name]`
make a new directory called `name`

`mkdir -p [level1/level2/...]`
allows you to create a series of nested directories by specifying a path using `-p` 

`cd`
used to change the directory **you** are currently located in

`cd ..`
goes to the directory above the current one

`cd ~`
goes to the home directory

`cd -`
goes to the previous directory

`cat [name]`
displays the specified file in the terminal

`./[name]`
used to execute a compiled program

`clear`
tmpties text in the terminal


# Directory Navigation in Linux
* If a path starts with a `~` or a `.` (dot), it is a *relative* path. If it starts with  a `/` , it is an *absolute* path.
    * Relative paths indicate that you are looking for a file or directory in relation to the directory you are currently in, while absolute paths give the full path to the directory from the root.
    * An absolute path with lead you to the same file or a directory regardless of your starting diretory or a user that uses it.
    * Accessing files using relative paths is often faster (to type :-)).

* Use the `..` command to reference previous/higher directories.
    * E.g.: `ls ../../` lists the contents of the parent directory of the parent directory of the directory you are currently in
        `cd ..` allows you to move back into the parent directory of the current one
* You will get an error if you try to access or reference a directory or file that does not exist!



**Relative Paths**
* `cd cs16/lab02` only works from one location, so it is a relative path
    * changing your current location anywhere from that one location will cause that path not to work (unless... what are the exceptions?)
    * `.` indicates that you are looking at a directory inside your current one, deeper than your current one
* `ls .` and `ls` do the same thing
* `ls ..` will show contents of the directory one level higher (not necessarily the previous directory -- do you know why?)
* `ls ../lab02` will go to the directory one level up, look for a directory called lab02, and then list the contents of that directory (if it exists)
* Can use ../../../ etc to go to higher-level directories as needed


**Absolute Paths**
* Absolute paths always start with a `/`.
* You can type in absolute paths with cd to skip typing cd several times in a row, if target file/directory is several directories deep
    * EX- `cd one`
            `cd two`
               `cd three`
    VS
        `cd /usr/ykk/labs/lab2/one/two/three`
* Make sure you know where the absolute path to a directory actually starts- you can use `pwd` to figure out where you are, which will give you the absolute path for the directory you are currently in (for the above example, `pwd` gives `/usr/ykk/labs/lab2`)

* Can also use absolute paths with other commands:
    `mkdir /home/jnewman/cs16/lab01`
    * If you didn’t have a cs16 directory in jnewman, then this command will create one. Then it will create a lab01 directory inside that new directory




* Imagine you start in your home directory, which holds several other directories.
    * Use `pwd` to determine which directory you are currently in, `ls` to see contents of the current directory
        * E.g.: If you are in the `home` directory, and you want to see the contents of `home`, then just use the command `ls` (this is a shortcut to `ls .`)
    * To see the contents of another directory without moving out of your current directory, you can use *paths*
        * E.g.: If you are in the `home` directory, which holds the `lab01` directory, and you want to look inside `lab01` without moving out of home, use the command `ls ./lab01` (or simply, `ls lab01`, because `lab01` is already in your current directory).
    * To copy a **directory**, use the command `cp -R [source] [destination]`
        * `-R` is a flag that indicates you are copying recursively and prepares cp to copy an entire directory
        * Don't use `-R` if you want to copy a file
        * You can use **absolute** or **relative** paths for either the source or destination directories
            * E.g.:
                With absolute as the first path and relative as the second path:
                   `cp -R /home/jgaucho/cs16/lab02 .`
                    * (the dot at the end indicates a relative path- copy the contents of the first directory into the current directory)
                With relative and relative, respectively:
                    `cp -R ./lab02  ../../jnewman`
                    * Grab lab02 directory from the current directory you are in (can also write it without `./` as just lab02)
                    * Can usually leave off `./` EXCEPT with executables- indicates that you are looking for an executable of that name in your current directory before you can run it
                With relative and absolute, respectively:
                    `cp -R ./lab02  /home/jnewman`

                    In the above examples, which directory were you in?


    *  `*` is the **wildcard** symbol (indicates that you want to perform an action on everything in a directory *that matches the given pattern*, e.g., if a pattern is `*.cpp`, then it will match everything that ends in `.cpp`; if the pattern is `hw0*`, then we will grab everything that starts with "hw0", e.g., `hw00.cpp`, `hw01.cpp`, etc.).



# Vim Commands

The link below is a very useful guide to learn fundamental "basic eight" commands in Vim:
<https://ucsb-cs16.github.io/topics/vim_basic_eight>


Here are some additional helpful commands in Vim (these are all done in the **Command Mode**)

* `dd` deletes the line the cursor is on
	- typing a number, such as 5, before `dd` deletes 5 lines starting from the cursor's location
* `p` pastes after the cursor of whatever is copied
	- `P` pastes before the cursor
* `yy` copies an entire line the cursor is on
	- a number `x` before `yy` copies `x` lines from the cursor (same as with `dd`)
* `%` finds the matching `{` or `(` if your cursor is on it
	- `d%` deletes everything between the `{` or `(` that the cursor is on and its match (i.e., `}` or `)`)
* `gg` goes to the 1st line of the file
* `G` goes to the last line of the file
* `u` undo (similar to ctrl + z or cmd + z on Word/Google Docs)
* `v` visual mode, this mode highlights the text 
	- `shift + v` visual line mode, highlights 1 horizontal line at a time
	- `ctrl + v` visual block mode, highlights 1 vertical line at a time
	- once you highlight text, you can copy it using `y` or delete it using `d`


# Writing, compiling and running a C++ program (hello world) program

```
// hello.cpp
#include <iostream>

using namespace std;

int main() {
	cout << "Hello CS 16!" << endl;
	return 0;
}
```

* Compile and execute the program

```
$ g++ -o hello hello.cpp
$ ./hello
Hello CS 16!
$
```

* `g++` is one of several C++ compilers
	* Compilers translate "source code" (i.e., the contents in the .cpp file) into a lower-level representation that is easier for computer system hardware to understand.
* `-o` is a "flag" that instructs the g++ compiler to produce an executable file called `hello`
* `hello.cpp` is the source file for g++ to use when producing the executable file.
* In order to actually run an executable file in Unix, `./[filename]` is used.




# Breaking down the Hello World Program

```
// hello.cpp
#include <iostream>

using namespace std;

int main() {
	cout << "Hello CS 16!" << endl;
	return 0;
}
```

```
#include <iostream>
```

* This line (also known as an _include directive_) tells our C++ program to include a library dealing with Input/Output (I/O) functionality.
	* We need the library `<iostream>` to print stuff to our terminal.

```
using namespace std;
```

* This line allows us to use parts of the iostream library without having to prepend `std::`.
	* For more context, `std` is short for "standard".
	* including libraries between angle brackets (< >) imply that this is part of the C++ Standard Library, which is part of the C++ language specification.

```
int main() { ... }
```

* The main function. Every C++ program needs to have one main function as its "starting point".

```
cout << "Hello CS 16!" << endl;
```

* `cout << [some_value]` tells the program to display some_value to the terminal.
* `<< endl;` tells the program to insert a <i>newline</i> at the end.
	* This places the next values to be written on the next line in the terminal.

```
return 0;
```

* Since main must be declared to return a value of "int" type, we are simply returning 0.
	* May get more into the relevance of this later.

# Comments

* Any commented text will be ignored by the compiler.
* Important to comment code for communication with others working with your code!
* `//` denotes a single-line comment.
* `/* */` denotes a multi-line comment.

# Practice Questions
1. Use what you know about Unix commands to accomplish the following, in order:
* Print your current working directory
* Create a file called `sample.txt` in your current directory
* While in your current directory, create a folder in your home directory called `helloWorld`
* Copy the file you just created, `sample.txt` into the home directory
* Navigate to the folder you just created from the home directory from part 3
* Move (not copy) `sample.txt` that's currently in the home directory from part 4
