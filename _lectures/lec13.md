---
num: "lect13"
lecture_date: 2019-05-16
desc: "Dynamic Memory; Nodes and Linked Lists"
ready: true
reading: "Chapters 9, 13.1"
---

### Dynamic memory / the heap / freestore

It's important to know the difference between the stack and the heap

The stack is where all local variables are stored - *variables on the stack are destroyed automatically when they go out of scope*

The heap is where all dynamic variables are stored - they are created with `new` and never go out of scope, but must be destroyed with the `delete` keyword (i.e., the programmer manages heap memory space manually).

**"new" operator**: The result of "new" is **a pointer to the object that was allocated on the heap**.

* Objects on the heap:
  * Don't have names, and can only be accessed by pointers
  * Can be lost forever if we lose their address (stored in a pointer). This is called a **memory leak**.
  * If you forget to `delete` stuff from the heap, you get a memory leak! Memory space is finite and eventually your program will crash if unused memory is not being deleted.


## Example of memory leaks

```
void g(int x) {
	int* p = new int(x);	// memory leak!
	delete p;		// remove this and see application size grow!
	return;
}

int main() {
for (int i = 0; i < 100000000; i++)
		g(i);
}
```

* since `int* p` in `g()` is a local variable, this gets removed from the stack, BUT THE VALUE ON THE HEAP REMAINS.
	* Once the variable is removed when the function exits, there is no way to remove this from the heap.
		* This is a memory leak!
* `delete` is the opposite of `new`
	* `new` creates an object on the heap and returns a pointer to it.
	* `delete` takes a pointer and removes the data from the heap.
		* `delete p;` doesn’t delete the variable p, it **deletes what p points to on the heap**!
		* `delete` only works for values that exist on the heap.

# Dangling Pointers
* After a pointer’s memory is deleted, the pointer itself is still available to use.
* BUT, you should never use a dangling pointer (the behavior of it is undefined).
	* And why would you want to use a pointer to something that shouldn’t be there?

## Dangling Pointers Example

```
int g(int x) {
	double* p = new double(x);
	delete p;	// delete value from the heap
	return *p; 	// p is a dangling pointer since heap contents were removed!
			// Results in undefined behavior. Shouldn’t do this!
}
```



### Example code: 

~~~cpp
int* p = new int;  //creates an integer on the heap and saves its address in p, created on the stack
delete p; //deallocates memory for that integer object. the value inside p is unchanged, but there is no object on the heap at that address

int size = 7; //size is an int created on the stack
int* a = new arr[size]; //creates an array on the heap of size 7, and saves the address of the first element in a.
delete [] a; //deallocates memory for the entire array
~~~

Re-writing above to introduce problems: depending on the compiler, the code might or might not produce an error after you try to use a dangling pointer (check what [Python Tutor](http://pythontutor.com/cpp.html#mode=edit) shows you :-)))

```cpp
#include <iostream>
using namespace std;

int main()
{
    int* p = new int;  //creates an integer on the heap and saves its address in p, created on the stack
    *p = 42;
    cout << &p << endl;
    cout << *p << endl;
    delete p; //deallocates memory for that integer object. the value inside p is unchanged, but there is no object on the heap at that address
    cout << &p << endl; // address of a dangling pointer
    cout << *p << endl;
    *p = 16;
    cout << &p << endl;
    cout << *p << endl;

    int size = 7; //size is an int created on the stack
    int* a = new int[size]; //creates an array on the heap of size 7, and saves the address of the first element in a.
    for (int i = 0; i < size; i++)
    {
        cout << a[0] << endl;

    }
    delete [] a; //deallocates memory for the entire array

    return 0;
}
```


## Lecture material
### Intro to Linked lists

> What are linked lists?

A linked list is a simple data structure that has nodes on the heap, and each node has a value and a pointer to the next node in the list.

A linked list itself has pointers to the first and last nodes (of the same type).


> Why use Linked lists?

Arrays are convenient because all elements are right next to each other in memory and can be quickly accessed.

But you cannot add new elements or quickly delete any - the size of an array is fixed, even of a dynamic one.

*A linked list is **not** a dynamic array!*
A dynamic array is just an array on the heap - they are different from regular arrays because their size can be defined at runtime, and they differ from linked lists because once the size is defined, the array stays at that size (until you potentially delete and resize it using `new []`).

Arrays aren’t good for everything!

### Structure of linked lists

* Nodes are not next to one another in memory and are only connected to each other by pointers.
* New elements can be inserted anywhere in the list by correctly reassigning pointers.

Every Linked List has a *head pointer* to the first node of that list and a *tail pointer* to the last node.
**In an empty linked list, head and tail pointers are both NULL.**

### Traversing linked lists
It turns out you can traverse through linked lists pretty easily!

* Set a pointer to a Node to the first Node of the Linked List (head).
* **Remember to always check if a Linked List is not empty** first! If you have an empty linked list, and you try to dereference the head, you will get a segfault!
* While you haven’t reached the end of the list, keep traversing - follow "next" pointers of every Node.
* You have reached the end of the list when the "next" pointer of the Node you are at is NULL.
* `for` loops or `while` loops will be super useful here!


```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

struct LinkedList {
    Node *head;
    Node *tail;
};

int main()
{
    // let's make a linked list with 1, 2, and 3 in it!
    Node *one = new Node;
    one->data = 1; // equivalent to (*one).data = 1;

    Node *two = new Node;
    two->data = 2; 

    Node *three = new Node;
    three->data = 3;

    one->next = two;
    two->next = three;
    three->next = NULL;

    LinkedList *l = new LinkedList;
    l->head = one;
    l->tail = three;

    return 0;
}
```


We will continue talking about Linked Lists in the next lectures.


# Midterm 2 Review

https://ucsb-cs16.github.io/s19-ykk/exam/e02/
