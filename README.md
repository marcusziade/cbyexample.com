# C by example
  * [Hello World](#hello-world)
  * [Types](#types)
  * [Initialization](#initialization)
  * [Comments](#comments)
  * [Switch](#switch)
  * [Array](#array)
  * [Strings](#strings)
  * [Functions](#functions)
  * [For Loops](#for-loops)
  * [While Loops](#while-loops)
  * [Goto](#goto)
  * [Integer Promotion](#integer-promotion)
  * [Program Arguments](#program-arguments)
  * [Storage Class Specifiers](#storage-class-specifiers)
  * [Type Qualifiers](#type-qualifiers)
  * [Inline Functions](#inline-functions)
  * [Conditional If](#conditional-if)
  * [Ternary Operator](#ternary-operator)
  * [Address Resolution Operator](#address-resolution-operator)
  * [Dereference Operator](#dereference-operator)
  * [Pointers](#pointers)
  * [Pointer Arithmetic](#pointer-arithmetic)
  * [Structs](#structs)
  * [Union](#union)
  * [Input & Output](#input--output)
  * [Bitwise Operations](#bitwise-operations)
  * [Typedef](#typedef)
  * [Enumerations](#enumerations)
  * [Variadic Functions](#variadic-functions)
  * [Threads](#threads)
  * [Mutex](#mutex)
  * [Heap Allocation](#heap-allocation)
  * [Assertions](#assertions)
  * [Compound Assignment](#compound-assignment)
  * [Project Structure](#project-structure)
  * [Includes](#includes)
  * [Compilation](#compilation)

## Hello World

```c
#include <stdio.h>

int main() {
	printf("Hello World!\n");
	return 0;
}
```

## Types
Every variable has an associated data type that defines its data storage format. Each type requires a certain amount of memory and permits a relevant set of operations.

```c
#include <stdbool.h>  //for bool

int main() {
	int a; // Integer
	unsigned int b; // Unsigned integers only store positive numbers. As a result, they have a higher positive range.
	char c; // Character
	short d; // Short integer
	long e; // Long integer
	float f; // Floating point integer
	double g; // Double-precision floating point integer
	bool h; // Boolean TRUE or FALSE
	return 0;
}
```

## Initialization

```c
int main() {
	int a = 0;
	char greeting_a[6] = {'H','e','l','l','o','\0'};
	char greeting_b[] = "Hello";
	char* greeting_c = "Hello";
	return 0;
}
```

## Comments
Comments are used to write notes and documentation that is to be ignored by the compiler at build time.

## Switch
Jump to a matching value. Usually cleaner to write than an if/else tree, and faster under the hood.

```c
#include <stdio.h>

int main() {
	int x = 2;
	switch(x) {
	case 1:
		printf("One");
		break; // You must break the search or it will fall through to the next match.
	case 2:
		printf("Two");
		break;
	default: // If no match is found.
		break;
	}
	return 0;
}
```
```
output: Two
```

## Array
An array is a collection of items stored at contiguous memory locations. Elements in an array can be accessed randomly using indices.

```c
#include <stdio.h>

int main() {
	int my_array[5];
	int my_array_b[] = {0,1,2,3,4}; // You can init the array from it's elements. Size can be detected automatically here.

	size_t len = sizeof(my_array) / sizeof(my_array[0]);
	for(size_t i = 0; i < len; i++) {
		my_array[i] = i;
	}

	printf("%d\n", my_array[2]);
	return 0;
}
```
```
output: 2
```

## Strings
A string is an array of characters. C++ supports **string** types natively, but in C, a string is an array of **char** data, terminated with the '\0' character.

```c
#include <stdio.h>

int main() {
	char* greeting_c = "Hello";
	return 0;
}
```

## Functions
Functions are re-usable code segments, created to perform specific tasks.

```c
#include <stdio.h>

// Double the number passed in as 'x', returning the new value to the function caller.
int double_number_a(int x) {
	return 2 * x;
}

// Double the number pointed to by 'x', storing the result in the original variable.
void double_number_b(int* x) {
	*x *= 2;
}

int main() {
	int num = 5;
	printf("%d\n", double_number_a(num));
	printf("%d\n", num);
	double_number_b(&num);
	printf("%d\n", num);
	return 0;
}
```
```
output: 10
        5
        10
```

## For Loops
Loops allow for continuous execution of a statement or group of statements, usually until a condition is met.

```c
#include <stdio.h>

int main() {
	for(int i = 1; i <= 3; i++) {
		printf("%d\n", i);
	}
	return 0;
}
```

## While Loops
Loops allow continuous execution of a statement or group of statements, usually until a condition is met.

```c
#include <stdio.h>

int main() {
	int x = 1;
	while(x <= 3) {
		printf("%d\n", x++);
	}
	return 0;
}
```

## Goto
Used to jump between code sections. The use of **goto** is contraversial as it can promote bad code decisions, but it can be very useful for avoiding large nested 'if' statements.

```c
#include <stdio.h>

int main() {
	int x;
	scanf("%d", &x);
	if (x < 3) goto cleanup;
	// Program code here
	cleanup:
	return 0;
}
```

## Integer Promotion
Any operand whose type ranks lower than int is temporarily promoted to int or unsigned int for comparison.

```c
#include <stdio.h>

int main() {
	char x = 'A';
	if (x < 'a') printf("Less than\n"); // x is promoted to int to compare it with the integer value of 'a'.
	else printf("Greater than or equal to\n");
	return 0;
}
```

## Program Arguments
A program can optionally take a set of arguments from the user at launch.

```c
#include <stdio.h>

int main(int argc, char* argv[]) {
	for(int i = 0; i < argc; i++) {
		printf("%s\n", argv[i]);
	}
	return 0;
}
```

## Storage Class Specifiers
Define the storage duration of an object.

```c
int main() {
	extern int a; // defined elsewhere
	static int b; // hold value between invocations
	register int c; // store in CPU register for fast access
	auto int d; // automatic duration - scope lifetime
	return 0;
}
```

## Type Qualifiers
A way of expressing additional information about a value through the type system to ensure correctness in the use of the data.

```c
int main() {
	restrict int* a; // Should only be accessed from this pointer
	const int b; // Once defined, is constant and cannot be changed
	atomic int c; // Can only be modified by one thread at a time
	volatile int d; // Can be modified externally. the program will check x's value before using it, even if it hasn't been modified locally.
	return 0;
}
```

## Inline Functions
Directly include the given function in the caller code sequence. This ensures that: function call overhead doesn’t occur ; overhead of push/pop variables on the stack is eliminated ; overhead of the return call is eliminated ; context-specific optimizations can be enabled at compile time.

```c
#include <stdio.h>

static inline void square(int* x) {
	*x *= *x;
	return;
}

int main() {
	int num = 5;
	square(&num);
	printf("%d\n", num);
	return 0;
}
```

## Conditional If
Responsible for modifying the flow of execution in a program. Always used with a condition, which is evaluated first before executing any statement inside the body.

```c
#include <stdio.h>

int main() {
	int x = 4;
	if (!x) printf("x is 0\n"); // one line if statement
	else if (x < 0) printf("x is negative\n");
	else { // or you can use a block			
		printf("x is positive\n");
	}
	return 0;
}
```

## Ternary Operator
A conditional operator that provides a shorter syntax for the **if** statement. The first operand is a boolean expression; if the expression is true then the value of the second operand is returned otherwise the value of the third operand is returned.

```c
#include <stdio.h>

int main() {
	int x = 4;
	x < 0 ? printf("x is negative\n") : printf("x is 0 or positive\n");
	return 0;
}
```

## Address Resolution Operator
Use '&' before a variable name to use it's address in memory rather than the value stored.

```c
#include <stdio.h>

int main() {
	int x = 5;
	printf("The address of x is %p\n", (void*)&x);
	return 0;
}
```

## Dereference Operator
Use '\*' before a variable name to use the value it points to rather than the address stored.

```c
#include <stdio.h>

int main() {
	int x = 4;
	int* y = &x;
	printf("The value stored at x is %d\n", *y);
	return 0;
}
```

## Pointers
A pointer is a variable that can hold the address of another variable. Just like regular data types, they must have their own type which refers to the type of the data at the address pointed to.

```c
#include <stdio.h>

int main() {
	int* x; // pointer to type int
	return 0;
}
```

## Pointer Arithmetic
Perform integer addition or subtraction operations on pointers, taking the data type's size into account to return the correct address of the next item.

```c
#include <stdio.h>

int main() {
	int x[5];
	int* x_ptr = &x[0];
	printf("Value of x_ptr = %p\n", (void*)x_ptr);
	printf("Value of x_ptr + 1 = %p\n", (void*)(x_ptr + 1));
	char y[5];
	char* y_ptr = &y[0];
	printf("Value of y_ptr = %p\n", (void*)y_ptr);
	printf("Value of y_ptr + 1 = %p\n", (void*)(y_ptr + 1));
	return 0;
}
```

## Structs
Structs are user defined data storage objects containing public members by default.

```c
#include <stdio.h>

struct my_struct {
	int x;
	int y;
};

int main() {
	struct my_struct object1;
	object1.x = 1;
	printf("%d\n", object1.x);
	return 0;
}
```

## Union
A union is a special data type that can store different data types at the same memory location. You can define a union with many members, but only one member can contain a value at any given time. Unions provide an efficient way of using the same memory location for multiple purposes. A union's size will be the size of the largest constituent type.

```c
#include <stdio.h>

union my_data {
	int i;
	float f;
	char str[20];
};
 
int main() {
	union my_data object1;        
	printf("Size of my_data union: %lu\n", sizeof(object1));
	return 0;
}
```

## Input & Output
In C, interacting with the user console is made possible through the **stdio.h** (standard input output library) header, which contains methods for input and output. C++ provides a convenient abstraction built into the **iostream** header, known as streams, to perform input and output operations in sequential media such as the screen, the keyboard or a file. A stream is an entity that a program can use to either insert or extract data.

```c
#include <stdio.h>

int main() {
	int x;
	printf("Enter an integer value for x: ");
	scanf("%d", &x);
	printf("The value at x is now: %d\n", x);
	return 0;
}
```

## Bitwise Operations
Bitwise operators are used to perform bit-level operations.

```c
#include <stdio.h>

int main() {
	unsigned char a = 5; // 00000101
	unsigned char b = 9; // 00001001
	printf("a & b = %d\n", a & b); // 00000001
	printf("a | b = %d\n", a | b); // 00001101
	printf("a ^ b = %d\n", a ^ b); // 00001100
	printf("~a = %d\n", a = ~a); // 11111010
	printf("b << 1 = %d\n", b << 1); // 00010010
	printf("b >> 1 = %d\n", b >> 1); // 00000100
	return 0;
}
```

## Typedef
Used to add an additional name to a type. Useful when working with more complex types, making them more human readable.

```c
#include <stdio.h>

typedef unsigned char byte;

int main() {
	byte b1 = 'c';
	return 0;
}
```

## Enumerations
A user-defined data type, used to assign names to integral constants to make a program easier to read and maintain.

```c
#include <stdio.h>

enum week {
	mon,
	tue,
	wed,
	thu,
	fri,
	sat,
	sun
};

int main() {
	for(int i = mon; i <= sun; i++)	{
		printf("%d\n", i); 
	} 
	return 0;
}
```
```
output: 0
        1
        2
        3
        4
        5
        6
```

## Variadic Functions
Create a function with an arbitrary argument count for more flexibility.

```c
#include <stdio.h>
#include <stdarg.h>

int sum(int count, ...)
{
	int total, i, temp;
	total = 0;
	va_list args;
	va_start(args, count);
	for(int i = 0; i < count; i++) {
		temp = va_arg(args, int);
        	total += temp;
	}
	va_end(args);
	return total;
}

int main() {
	int numbers[3] = {5, 10, 15};
	int sum_of_numbers = sum(3, numbers[0], numbers[1], numbers[2]);
	printf("Sum of the array: %d\n", sum_of_numbers);
	return 0;
}
```
```
output: Sum of the array: 30
```

## Threads
Used to execute one or more subthreads to allow for parallel processing in the same memory space, usually resulting in a performance improvement in a larger program.

```c
#include <stdio.h>
#include <threads.h>

int thread_func(void* arg) { 
	printf("Printing from Thread\n"); 
	return NULL;
} 
   
int main() { 
	thrd_t thread_id; 
	thrd_create(&thread_id, thread_func, NULL); 
	thrd_join(thread_id, NULL);  // Wait for thread to return before continuing execution
	printf("Thread returned\n"); 
	return 0;
}
```
```
output: Printing from Thread
        Thread returned
```

## Mutex
Mutual exclusion functionality. Can be used to serialize access of shared variables between concurrent threads.

```c
#include <stdio.h>
#include <threads.h>

typedef struct data {
	mtx_t mtx;
	int x;
} data;

int thread_func(void* arg) { 
	data* d = (data*)arg;
	mtx_lock(&d->mtx);	
	d->x = 2;	
	mtx_unlock(&d->mtx);
	return 0;
} 
   
int main() {
	data d;
	mtx_init(&d.mtx, mtx_plain);
	thrd_t thread_id; 
	thrd_create(&thread_id, thread_func, (void*)&d); 
	thrd_join(thread_id, NULL);  // Wait for thread to return before continuing execution
	printf("x has safely been modified to %d\n", d.x); 
	return 0;
}
```

## Heap Allocation
Memory can be allocated on the heap, an unreserved and relatively large region of memory outside of the program's memory scope.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	int* x = (int*)malloc(sizeof(int)); // pointer to a heap-reserved integer
	if (x) { // test that the memory was allocated before you use it
		free(x); // you must manually free any memory you allocated on the heap or it will persist (memory leak)
	}
	return 0;
}
```

## Assertions
Statements used to explicitly test assumptions made by the programmer. Will be checked at runtime, or if static at compile time. A powerful tool for statement or unit testing.

```c
#include <stdio.h>
#include <assert.h>

int main() {
	int x = 1;
	assert(x == 2); // this should break the execution of the program
	return 0;
}
```
```
output: int main(): Assertion `x == 2' failed. 
```

## Compound Assignment
Provides a shorter syntax for assigning the result of an arithmetic or bitwise operator by performing an operation on the two operands before assigning the result to the first operand.

```c
#include <stdio.h>

int main() {
	int x = 1;
	x += 1;
	printf("x = %d\n", x);
	return 0;
}
```
```
output: x = 2
```

## Project Structure
It's useful to follow a conventional and sensible structure when organizing a project, to maintain readability.

```
myproject/src/main.c // main function
myproject/include/file.c // function definitions etc
myproject/include/file.h // structs, function prototypes etc
myproject/Makefile // automated project build file
myproject/README.md // store any useful documentation or links to documentation in here
myproject/obj/file // temporary object files
myproject/bin/file // executable output from compiler
```

## Includes
Includes are instructions to the preprocessor to include external code. External code is made up of at least a header file (interface) and a source file (implementation).

When compiling your program, **#include** the header, and link the source file at compile time.

In file src/main.c
```c
#include <stdio.h> // Include a dependency from the system library
#include "../include/file.h" // Include a local dependency from a relative path

int main() {
	// Use file.h
}
```
In file include/file.c:
```c
#include <stdio.h> // Include a dependency from the system library
#include "file.h" // Include a local dependency from a relative path
```
In file include/file.h:
```c
#ifndef PROG_H // Only process the below if it hasn't already been processed in the current compilation.
#define PROG_H

// File contents here

#endif
```

## Compilation
Compiling source code turns it into machine language through preprocessing, compiling, assembly and linking.


```
gcc -c -std=c17 src/main.c -o obj/main.o // Compile main.c to object
gcc -c -std=c17 include/file.c -o obj/file.o // Compile file.c to object
gcc obj/main.o obj/file.o -o bin/prog // Link objects and create executable bin/prog
```
```
output: Cannot divide by 0
```
Copyright &copy; 2022 Marcus Ziadé | [Source](https://github.com/marcusziade/cbyexample.com "Source")
## Forked from https://github.com/seanvaleo/cbyexample.com
## This version has the C++ part removed
