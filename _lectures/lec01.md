---
num: "lect01"
lecture_date: 2019-04-02
desc: "Introductions and Course overview"
ready: true
pdfurl: https://drive.google.com/open?id=1zP7YNmZXCYnAP8MrEiaf1Ov28ESpXR0s
---

# Course Logistics

* If you have not yet, go and familiarize yourself with the syllabus.
* Due to the large amount of emails, it may take a while for Prof. K to respond
* Because of this, please add "CS 16" to the title of every email
* For 1-on-1 help, tutors and TAs are available during closed and open lab hours (open lab hours will begin during week 2)

***

# Parts of a Computer

A computer can be divided into two major parts, hardware and software
* Hardware is the physical parts of the computer, like the CPU, RAM, etc.
* Software are the data instructions that runs on the hardware, like the operating system and programs

In an abstract view, a computer can be divided into 5 hardware components
1. Input devices
   * This is your keyboard, mouse, microphone, touchscreen, anything that you input data to the computer
2. Output devices
   * This is your monitor, speakers, anything that the computer outputs data to
3. Processor
   * The CPU. This is the brain of the computer, and it's where calculations are getting done
4. Main memory
   * The is your RAM (random-access memory), ROM (read-only memory), etc.
   * The main memory is volatile, meaning that data is lost when the computer powers down
5. Secondary memory
   * This is your storage, like hard drives/SSDs
   * Secondary memory is significantly slower, but is non-volatile: the data is saved even when the computer is off
  
This method to divide a computer into theses 5 parts is known as the von Neumann architecture

***

# Basic Structure of a C++ Program

C++ file containing C++ code has the filename extension `.cpp`

A basic C++ program usually looks like the following

```
#include <iostream> //This adds the basic input/output functions

using namespace std;  //This clarifies the functionality of iostream

int main()
{
  //Write your code here
  
  
  return 0; //This ends the program, and indicates the program has finished successfully
}
```

In your program, you want to return a non-zero number to indicate that a program terminated abnormally

***

# The C++ Compilation Process

Compared to Python, where you write and then run the code under IDLE, C++ programs must be compiled.

During the compilation process, a compiler turns the program you write into something a computer understands (binary code).

Therefore, you end up with 3 parts of creating a program in C++:
1. Editing: writing the code in a text file
2. Compiling: translating the code to something a computer can understand (a binary version of the code)
3. Running: executing the binary version of the code on the computer

Later on in the course we will learn more tricks to save time compiling. For a small program, re-compiling may take a small amount of time, but for large programs, anything we can optimize will speed up the compile time, like only re-compiling the files we changed.
