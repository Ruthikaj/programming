Q1. What is C programming language?

Answer: C is a general-purpose programming language that was developed by Dennis Ritchie at Bell Labs in 1972. It is widely used for system programming, developing operating systems, and embedded systems due to its close association with hardware.
2. Explain the basic structure of a C program.

Answer:

    Header Files: #include <stdio.h>
    main() function: Entry point of a C program.
    Code inside main() is executed.

3. What is the use of printf() and scanf() in C?

Answer:

    printf() is used for output.
    scanf() is used for input.

4. Explain different data types in C.

Answer:

    int: Integers.
    float: Floating-point numbers.
    char: Characters.
    double: Double-precision floating-point numbers.

5. What are variables?

Answer: Variables are containers for storing data values. Each variable must have a unique name and a data type.
6. What is the difference between = and == in C?

Answer:

    = is the assignment operator.
    == is the equality comparison operator.

7. What is a pointer in C?

Answer: A pointer is a variable that stores the memory address of another variable.
8. What is NULL pointer in C?

Answer: A NULL pointer is a pointer that doesn’t point to any valid memory location. In C, it is often defined as (void*)0.
9. How do you declare an array in C?

Answer: int arr[10]; declares an array of size 10.
10. What is a string in C?

Answer: A string in C is a one-dimensional array of characters terminated by a null character (\0).
11. What is a function in C?

Answer: A function is a block of code that performs a specific task and can be called repeatedly.
12. What is recursion in C?

Answer: Recursion is the process in which a function calls itself directly or indirectly.
13. What is the syntax for a for loop in C?

Answer:

Copy code

for (initialization; condition; increment/decrement) {
    // Code
}

14. What are control structures?

Answer: Control structures include loops (for, while, do-while), and conditional statements (if, else, switch).
15. How do you define a constant in C?

Answer: Using #define or the const keyword.
16. What is typecasting?

Answer: Typecasting is the conversion of one data type into another.
17. What is the difference between break and continue?

Answer:

    break: Exits the loop.
    continue: Skips the current iteration and moves to the next iteration.

18. What is a switch statement?

Answer: The switch statement tests a variable against multiple cases and executes the matching case.
19. What is the difference between local and global variables?

Answer:

    Local: Declared inside a function/block.
    Global: Declared outside all functions and is accessible throughout the program.

20. What is the use of the sizeof() operator?

Answer: sizeof() returns the size of a data type or variable in bytes.
21. What is the syntax of a while loop in C?

Answer:

Copy code

while (condition) {
    // Code
}

22. Can you explain what a do-while loop is?

Answer: A do-while loop is similar to a while loop, but it executes the code at least once before checking the condition.
23. What is the difference between ++i and i++?

Answer:

    ++i: Pre-increment (increments value before use).
    i++: Post-increment (uses value, then increments).

24. What is a structure in C?

Answer: A structure is a user-defined data type that groups different data types together.
25. What are command-line arguments?

Answer: Command-line arguments are parameters passed to main() when the program is executed.
Intermediate Level
26. What is memory leakage? How can it be prevented?

Answer: Memory leakage occurs when a program allocates memory dynamically but fails to free it. It can be prevented by using free() to deallocate memory.
27. What are the storage classes in C?

Answer:

    auto: Local variable.
    register: Fast access local variable.
    static: Retains value across function calls.
    extern: Global variable declaration.

28. What is a static function?

Answer: A static function can only be called within the file it is declared, providing limited scope.
29. What is malloc() in C?

Answer: malloc() dynamically allocates memory at runtime and returns a pointer to the allocated memory.
30. What is the difference between malloc() and calloc()?

Answer:

    malloc(): Allocates uninitialized memory.
    calloc(): Allocates initialized memory (all bytes set to zero).

31. What is a dangling pointer?

Answer: A pointer that points to a memory location that has been freed.
32. How do you prevent a dangling pointer?

Answer: Set the pointer to NULL after freeing the memory.
33. What is the use of the free() function?

Answer: It deallocates previously allocated memory to prevent memory leaks.
34. What is a void pointer?

Answer: A void pointer is a generic pointer that can point to any data type.
35. Explain bitwise operators.

Answer: Bitwise operators perform operations on binary representations of integers.

    &: AND
    |: OR
    ^: XOR
    ~: NOT
    <<: Left shift
    >>: Right shift

36. What is a macro?

Answer: A macro is a fragment of code defined with #define, which gets replaced by its value during preprocessing.
37. What is the difference between const and volatile variables?

Answer:

    const: Value can’t be changed.
    volatile: The value can be changed unexpectedly (e.g., by hardware).

38. What is typedef in C?

Answer: typedef is used to create alias names for existing data types.
39. What is a linked list?

Answer: A linked list is a data structure where each element (node) contains a data part and a pointer to the next node.
40. How do you create a singly linked list in C?

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};int main() {
    struct Node *head = NULL;
    head = (struct Node*)malloc(sizeof(struct Node));
    head->data = 1;
    head->next = NULL;
    return 0;
}

41. What is a double pointer in C?

Answer: A double pointer is a pointer to a pointer, often used for dynamic memory allocation.
42. What is the difference between struct and union?

Answer:

    struct: Allocates memory for all members.
    union: Allocates memory for the largest member, and all members share the same memory.

43. What is a function pointer?

Answer: A function pointer is a pointer that points to the address of a function, allowing functions to be passed as arguments.
44. What is typecasting in C?

Answer: Typecasting is the conversion of one data type into another, either implicitly or explicitly.
45. Explain the enum data type in C.

Answer: enum is a user-defined data type that assigns names to integer constants.
Advanced Level
46. What are the key features of C language?

Answer: Simple, efficient, low-level access to memory, structured programming, portability.
47. What is a preprocessor in C?

Answer: The preprocessor processes the code before compilation, handling directives like #include, #define, #ifdef, etc.
48. Explain dynamic memory allocation.

Answer: Dynamic memory allocation allocates memory at runtime using functions like malloc(), calloc(), and realloc().
49. What is the difference between exit() and _Exit()?

Answer:

    exit(): Performs cleanup functions before exiting.
    _Exit(): Terminates the program immediately without cleanup.

50. What is the volatile keyword in C?

Answer: volatile tells the compiler not to optimize the code for variables that may change unexpectedly, like hardware registers.

Q2. Mention the different storage classes in C.

This might be one of the most debated C interview questions; the answer to this question varies book by book, and site by site on the internet. Here, I would like to make it clear there are only two storage classes in C, and the rest are storage class specifiers.

As per reference manual of “The C Programming Language” by: Brian W. Kernighan and Dennis M. Ritchie, in the Appendix A of the reference manual, the very first line says: There are two storage classes: automatic and static.
[The C programing Language 2nd Edition,Brian W. Kernighan ,Dennis M. Ritchie ]

Q51. What are the different storage class specifiers in C?

There are 4 storage class specifiers in C, out of which auto and static act as storage classes as well. So, the storage class specifiers are:

    Auto
    Register
    Static
    Extern

Q3. What are library functions in C?

Library functions are the predefined functions in C, stored in .lib files.

Q4. Where are the auto variables stored?

Auto variables are stored in the main memory. The default value of auto variables is garbage value.

Q5. What is the difference between i++ and ++i?

One of the most commonly asked C interview questions or viva questions — i++ and ++i. The expression i++ returns the old value and then increases i by 1, whereas the expression ++i first increases the value of i by 1 and then returns the new value.

Q6. What is l-value in C? Mention its types.

Location value, commonly known as the l-value, refers to an expression used on the left side of an assignment operator. For example: in the expression “x = 5”, x is the l-value and 5 is the r-value.

There are two types of l-value in C — modifiable l-value and non-modifiable l-value. modifiable l-value denoted a l-value which can be modified. non-modifiable l-value denote a l-value which cannot be modified. const variables are non-modifiable l-value.

Q7. Can i++ and ++i be used as l-value in C?

In C both i++ and ++i cannot be used as l-value. Whereas in C++, ++i can be used as l-value, but i++ cannot be.

Q8. Which of the following shows the correct hierarchy of arithmetic operations in C?

(1) / + * –
(2) * — / +
(3) + — / *
(4) * / + –

4 is the correct answer.

Q9. Which bit wise operator is suitable for

    checking whether a particular bit is on or off?
    Ans. The bitwise AND operator.
    turning off a particular bit in a number?
    Ans. The bitwise AND operator.
    putting on a particular bit in a number?
    Ans. The bitwise OR operator.

Q10. Can a C program be written without using the main function?

This is one of the most interesting C interview questions. I guess, up until now, you might not have ever written a C program without using the main function. But, a program can be executed without the main function. See the example below:

#include<stdio.h>
#define decode(s,t,u,m,p,e,d) m##s##u##t
#define begin decode(a,n,i,m,a,t,e)
int begin()
{
    printf(” hello “);
}

Now, lets see what’s happening within the source code. Here, #define acts as the main function to some extent. We are basically using #define as a preprocessor directive to give an impression that the source code executes without the main function.

Q11. What is the output of printf(“%d”); ?

For printf(“%d”, a); the compiler will print the corresponding value of a. But in this case, there is nothing after %d, so the compiler will show garbage value in output screen.

Q12. What is the difference between printf() and sprintf() ?

printf() statement writes data to the standard output device, whereas sprintf() writes data to the character array.

Q13. What is the difference between %d and %*d ?

Here, %d gives the original value of the variable, whereas %*d gives the address of the variable due to the use of pointer.

Q14. Which function — gets() or fgets(), is safe to use, and why?

Neither gets() nor fgets() is completely safe to use. When compared, fgets() is safe to use than gets() because with fgest() a maximum input length can be specified.

Q15. Write a C program to print “Programming is Fun” without using semicolon (;) .

Here’s a typical source code to print “Programming is Fun”.

#include<stdio.h>
int main()
{
      printf("Programming is Fun");
      return 0;
}

There’s not much trick in printing the line without using the semicolon. Simply use the printf statement inside the if condition as shown below.

#include<stdio.h>
int main()
{
      if( printf( "Programming is Fun" ) )
      {    }
}

An extension of the above can be — write a C program to print “;” without using a semicolon.

#include<stdio.h>
int main()
{
   if(printf("%c",59))
   {
   }
}

Q16. What is the difference between pass by value and pass by reference?

This is another very important topic in this series of C interview questions. I will try to explain this in detail with source code and output.

Pass by Value:

This is the process of calling a function in which actual value of arguments are passed to call a function. Here, the values of actual arguments are copied to formal arguments, and as a result, the values of arguments in the calling function are unchanged even though they are changed in the called function. So, passing by value to function is restricted to one way transfer of information. The following example illustrates the mechanism of passing by value to function.

#include<stdio.h>
void swap(int a, int b)
{
    int temp ;
    temp=a;
    a=b;
    b=temp;
}
main()
{
    int x, y,sum;
prinft(“Enter x and y : );
    scanf(“%d%d”,&x,&y);
    printf(“ Before swap, x=%d, y=%d”, x,y)
    swap(x,y);
    printf(“After swap, x=%d, y=%d”, x,y)
}

//Output:
Enter x and y: 5  10
Before swap, x=5, y=10
After swap, x=5, y=10//

In this example, the values of x and y have been passed into the function and they have been swapped in the called function without any change in the calling function.

Pass by Reference:

In pass by reference, a function is called by passing the address of arguments instead of passing the actual value. In order to pass the address of an argument, it must be defined as a pointer. The following example illustrates the use of pass by reference.

#include<stdio.h>
void swap(int a*, int b*);
main()
{
    int x, y,sum;
prinft(“Enter x and y : );
    scanf(“%d%d”,&x,&y);
    printf(“ Before swap, x=%d, y=%d”, x,y)
    swap(&x, &y);
    printf(“After swap, x=%d, y=%d”, x,y)
}
void swap(int *a, int *b)
{
    int temp ;
    temp=*a;
    *a=*b;
    *b=temp;
}

//Output:
Enter x and y: 5  10
Before swap, x=5, y=10
After swap, x=10, y=5//

In this example, addresses of x and y have been passed into the function, and their values are swapped in the called function. As a result of this, the values are swapped in calling function also.

Q17. Write a C program to swap two variables without using a third variable.

This is one of the very common C interview questions. It can be solved in a total of five steps. For this, I have considered two variables as a and b, such that a = 5 and b = 10.

#include<stdio.h>
int main(){
    int a=5,b=10;

    a=b+a;
    b=a-b;
    a=a-b;
    printf("a= %d  b=  %d",a,b);    a=5;
    b=10;
    a=a+b-(b=a);
    printf("\na= %d  b=  %d",a,b);    a=5;
    b=10;
    a=a^b;
    b=a^b;
    a=b^a;
    printf("\na= %d  b=  %d",a,b);
   
    a=5;
    b=10;
    a=b-~a-1;
    b=a+~b+1;
    a=a+~b+1;
    printf("\na= %d  b=  %d",a,b);
   
    a=5,
    b=10;
    a=b+a,b=a-b,a=a-b;
    printf("\na= %d  b=  %d",a,b);
    return 0;
}

Q18. When is a switch statement better than multiple if statements?

When two or more than two conditional expressions are based on a single variable of numeric type, a switch statement is generally preferred over multiple if statements.

Q19. Write a C program to print numbers from 1 to n without using loop.

void printNos(unsigned int n)
{
  if(n > 0)
  {
    printNos(n-1);
    printf("%d ",  n);
  }
}

Q20. What is the difference between declaration and definition of a function?

Declaration of a function in the source code simply indicates that the function is present somewhere in the program, but memory is not allocated for it. Declaration of a function helps the program understand the following:

    what are the arguments to that function
    their data types
    the order of arguments in that function
    the return type of the function

Definition of a function, on the other hand, acts like a super set of declaration. It not only takes up the role of declaration, but also allocates memory for that function.

Q21. What are static functions? What is their use in C?

In the C programming language, all functions are global by default. Therefore, to make a function static, the “static” keyword is used before the function. Unlike the global functions, access to static functions in C is restricted to the file where they are declared.

The use of static functions in C are:

    to make a function static
    to restrict access to functions
    to reuse the same function name in other file

Q22. Mention the advantages and disadvantages of arrays in C.

Advantages:

    Each element of array can be easily accessed.
    Array elements are stored in continuous memory location.
    With the use of arrays, too many variables need not be declared.
    Arrays have a wide application in data structure.

Disadvantages:

    Arrays store only similar type of data.
    Arrays occupy and waste memory space.
    The size of arrays cannot be changed at the run time.

Q23. What are array pointers in C?

Array whose content is the address of another variable is known as array pointer. Here’s an example illustrating array pointers in C.

int main()
{
    float a=0.0f,b=1.0f,c=2.0f;
    float * arr[]= {&a,&b,&c};
    b=a+c;
    printf("%f",arr[1]);
    return 0;
}

Q24. How will you differentiate char const* p and const char* p ?

In char const* p, the pointer ‘p’ is constant, but not the character referenced by it. Here, you cannot make ‘p’ refer to any other location, but you can change the value of the char pointed by ‘p’.

In const char* p, the character pointed by ‘p’ is constant. Here, unlike the upper case, you cannot change the value of character pointed by ‘p’, but you can make ‘p’ refer to any other location.

Q25. What is the size of void pointer in C?

Whether it’s char pointer, function pointer, null pointer, double pointer, void pointer or any other, the size of any type of pointer in C is of two byte. In C, the size of any pointer type is independent of data type.

Q26. What is the difference between dangling pointer and wild pointer?

Both these pointers don’t point to a particular valid location.

A pointer is called dangling if it was pointing to a valid location earlier, but now the location is invalid. This happens when a pointer is pointing at the memory address of a variable, but afterwards some variable has been deleted from that particular memory location, while the pointer is still pointing at that memory location. Such problems are commonly called dangling pointer problem and the output is garbage value.

Wild pointer too doesn’t point to any particular memory location. A pointer is called wild if it is not initialized at all. The output in this case is any address.

Q27. What is the difference between wild pointer and null pointer?

Wild pointer is such a pointer which doesn’t point to any specific memory location as it is not initialized at all. Whereas, null pointer is the one that points the base address of segment. Literally, null pointers point at nothing.

Q28. What is far pointer in C?

Far pointer is the pointer that can access all the 16 segments, i.e. the whole residence memory of RAM. The size of far pointer is 4 byte. The example below illustrates the size of far pointer in C.

int main()
{
    int x=10;
    int far *ptr;
    ptr=&x;
    printf("%d",sizeof ptr);
    return 0;
}
//Output: 4

Q29. What is FILE?

FILE is simply a predefined data type defined in stdio.h file.

Q30. What are the differences between Structure and Unions?

    Every member in structure has its own memory, whereas the members in a union share the same member space.
    Initialization of all the member at the same time is possible in structures but not in unions.
    For the same type of member, a structure requires more space than a union.
    Different interpretations of the same memory space is possible in union but not in structures.

Q31. Write a C program to find the size of structure without using sizeof operator?

struct  ABC
{
    int a;
    float b;
    char c;
};
int main()
{
    struct ABC *ptr=(struct ABC *)0;
    ptr++;
    printf("Size of structure is: %d",*ptr);
    return 0;
}

Q32. What is the difference between .com program and .exe program?

Both these programs are executable programs, and all drivers are .com programs.

    .com program executes faster than .exe program.
    .com file has higher preference than .exe type.

Some Interesting C Interview Questions:

1. Why does n++ execute faster than n+1 ?

The execution depends on the amount machine instruction to carry out the operation in the expression. n++ requires only a single machine instruction, such as INR, to carry out the increment operation. On the other hand, n+1 requires more machine instructions to carry out this operation. Hence, n++ executes faster than n+1 in C.

2. Is int x; a declaration or a definition? What about int x = 3; and x = 3; ?

int x; is a declaration. int x = 3; is a declaration with initialization/definition of variable x with a value. x = 3; is a definition.

3. What is the parent of the main() function?

The parent of main() function is header files — the <stdio.h> header file.

4. Write a C program to print the next prime number for any number entered by the user.

#include< stdio.h>
#include< conio.h>
void main()
{
    int i,j=2,num;
    clrscr();
    printf("Enter any number: ");
    scanf("%d",&num);
    printf("Next Prime number: ");
    for(i=num+1; i< 3000; i++)
    {
        for(j=2; j< i; j++)
        {
            if(i %j==0)
            {
                break;
            } // if
        } // for
        if(i==j || i==1)
        {
            printf("%d\t",i);
            break;
        }// if
    }// outer for getch();
}

5. Write a C program to solve the “Tower of Hanoi” question without using recursion.

Try this yourself.

6. Create an array of char type whose size is not known until its run, i.e., the size must be given by the user.

Hints are given in the source code below. If you want to use array finish, you must free it to return resources to memory.

char *sz = NULL;
int i = 0; 
scanf("%d", i );
if(i){ sz = (char *)malloc( sizeof(char)*i);
