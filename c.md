### 1. Which of the following is the correct syntax to declare a variable in C?
- A) `int var_name;`
- B) `var int;`
- C) `variable int var_name;`
- D) `declare int var_name;`

**Answer:** A

### 2. What is the size of `int` data type in C?
- A) 2 bytes
- B) 4 bytes
- C) 8 bytes
- D) 1 byte

**Answer:** B

### 3. Which of the following is not a valid C variable name?
- A) `var1`
- B) `_var_name`
- C) `1var`
- D) `var_name`

**Answer:** C

### 4. Which keyword is used to prevent any changes in the variable within a C program?
- A) `const`
- B) `volatile`
- C) `static`
- D) `extern`

**Answer:** A

### 5. What is the output of the following code?
```c
int a = 10, b = 20;
printf(“%d”, a > b ? a : b);
```
- A) 10
- B) 20
- C) 0
- D) None of the above

**Answer:** B

### 6. Which of the following is a logical operator in C?
- A) `+`
- B) `&&`
- C) `=`
- D) `!=`

**Answer:** B

### 7. The default return type of a function in C is:
- A) `void`
- B) `char`
- C) `int`
- D) `float`

**Answer:** C

### 8. What will be the output of the following program?
```c
#include<stdio.h>
int main() {
int x = 5;
if(x == 5) printf(“Hello”);
else printf(“World”);
return 0;
}
```
- A) Hello
- B) World
- C) Compilation Error
- D) None of the above

**Answer:** A

### 9. Which of the following is used to terminate a function in C?
- A) `break`
- B) `return`
- C) `exit`
- D) `continue`

**Answer:** B

### 10. What is the maximum number of arguments that a function can take in C?
- A) 127
- B) 253
- C) 255
- D) 32767

**Answer:** C

### 11. How many bytes does a pointer occupy in C on a 32-bit machine?
- A) 2
- B) 4
- C) 8
- D) 1

**Answer:** B

### 12. What is the correct way to declare a pointer to an integer in C?
- A) `int *ptr;`
- B) `int ptr;`
- C) `int &ptr;`
- D) `int ptr*;`

**Answer:** A

### 13. What will be the output of the following code?
```c
#include<stdio.h>
int main() {
int x = 10;
printf(“%d”, ++x);
return 0;
}
```
- A) 9
- B) 10
- C) 11
- D) Compilation error

**Answer:** C

### 14. Which of the following functions is used to allocate memory dynamically in C?
- A) `malloc()`
- B) `alloc()`
- C) `alloc_mem()`
- D) `new()`

**Answer:** A

### 15. What does the `sizeof` operator return in C?
- A) Size of data type in bits
- B) Size of data type in bytes
- C) Address of variable
- D) None of the above

**Answer:** B

### 16. Which of the following is not a storage class in C?
- A) `register`
- B) `auto`
- C) `dynamic`
- D) `static`

**Answer:** C

### 17. Which loop will execute at least once, even if the condition is false?
- A) `for`
- B) `while`
- C) `do-while`
- D) None of the above

**Answer:** C

### 18. What is the output of the following code?
```c
#include<stdio.h>
int main() {
int a = 5, b = 10;
printf(“%d”, a = b);
return 0;
}
```
- A) 5
- B) 10
- C) 0
- D) Compilation error

**Answer:** B

### 19. What will be the output of the following code?
```c
#include<stdio.h>
int main() {
int i;
for(i=0; i<5; i++);
printf(“%d”, i);
return 0;
}
```
- A) 4
- B) 5
- C) 6
- D) Compilation error

**Answer:** B

### 20. Which header file is required for input/output functions in C?
- A) `stdlib.h`
- B) `conio.h`
- C) `stdio.h`
- D) `math.h`

**Answer:** C

### 21. The result of the expression `sizeof(char)` is:
- A) 1
- B) 2
- C) 4
- D) Depends on the compiler

**Answer:** A

### 22. In which of the following header files is the function `strcmp()` declared?
- A) `string.h`
- B) `strings.h`
- C) `strcmp.h`
- D) `stdlib.h`

**Answer:** A

### 23. The keyword used to define a constant in C is:
- A) `const`
- B) `define`
- C) `constant`
- D) `static`

**Answer:** B

### 24. Which operator is used to access the address of a variable in C?
- A) `*`
- B) `&`
- C) `->`
- D) `.`

**Answer:** B

### 25. What is the file extension of C programming language source file?
- A) `.cpp`
- B) `.c`
- C) `.obj`
- D) `.exe`

**Answer:** B

### 26. What is the output of the following code?
```c
#include<stdio.h>
int main() {
int arr[3] = {1, 2, 3};
printf(“%d”, arr[1]);
return 0;
}
```
- A) 1
- B) 2
- C) 3
- D) Compilation error

**Answer:** B

### 27. What is a correct syntax to define a structure in C?
- A) `struct { int x; float y; };`
- B) `struct { x, y; };`
- C) `struct int { int x; float y; };`
- D) `structure { int x; float y; };`

**Answer:** A

### 28. What is a `union` in C programming?
- A) A structure that allocates memory dynamically
- B) A memory location that stores multiple data types
- C) A structure that allocates shared memory for members
- D) None of the above

**Answer:** C

### 29. What does the following declaration represent?
```c
int *ptr;
```
- A) `ptr` is a pointer to an integer
- B) `ptr` is a pointer to a float
- C) `ptr` is a pointer to a character
- D) `ptr` is a pointer to a pointer

**Answer:** A

### 30. Which of the following is not a valid preprocessor directive?
- A) `#include`
- B) `#define`
- C) `#undef`
- D) `#main`

**Answer:** D

Here are the remaining questions (31–50) for C programming interviews:

### 31. What will be the output of the following code?
```c
#include<stdio.h>
int main() {
int x = 5;
printf(“%d”, x++);
return 0;
}
```
- A) 4
- B) 5
- C) 6
- D) Undefined

**Answer:** B

### 32. Which of the following functions is used to free dynamically allocated memory?
- A) `free()`
- B) `delete()`
- C) `release()`
- D) `clear()`

**Answer:** A

### 33. What is the purpose of `&` operator in C?
- A) It returns the address of a variable
- B) It performs bitwise AND operation
- C) It returns the value stored in the pointer
- D) Both A and B

**Answer:** D

### 34. Which of the following operators is used to dereference a pointer?
- A) `&`
- B) `*`
- C) `->`
- D) `.`

**Answer:** B

### 35. What is the default value of an uninitialized local variable in C?
- A) `0`
- B) `Garbage value`
- C) `NULL`
- D) Depends on the compiler

**Answer:** B

### 36. What is the output of the following program?
```c
#include<stdio.h>
int main() {
int i;
for(i = 0; i < 5; ++i) {
if(i == 3)
continue;
printf(“%d”, i);
}
return 0;
}
```
- A) 01234
- B) 0124
- C) 1234
- D) 0134

**Answer:** D

### 37. Which of the following data types will occupy more memory in C?
- A) `int`
- B) `float`
- C) `char`
- D) `double`

**Answer:** D

### 38. What will be the output of the following code?
```c
#include<stdio.h>
int main() {
printf(“%d”, sizeof(3.14));
return 0;
}
```
- A) 4
- B) 8
- C) 2
- D) 10

**Answer:** B

### 39. Which of the following is the correct way to declare a function in C?
- A) `int func(int x, float y);`
- B) `func(int x, float y) int;`
- C) `int func(int x float y);`
- D) `func(int x, float y);`

**Answer:** A

### 40. What is recursion in C programming?
- A) A function calling another function
- B) A function calling itself
- C) Multiple loops within a function
- D) A function with multiple return types

**Answer:** B

### 41. What is the output of the following program?
```c
#include<stdio.h>
int main() {
int a = 10, b = 5;
printf(“%d”, a % b);
return 0;
}
```
- A) 1
- B) 5
- C) 0
- D) Compilation error

**Answer:** C

### 42. What is the purpose of the `static` keyword in C?
- A) To define a constant value
- B) To make a variable persist across function calls
- C) To define a local variable
- D) To prevent a function from returning a value

**Answer:** B

### 43. Which of the following statements is true about `switch` statements?
- A) `switch` accepts `float` values
- B) `switch` does not allow duplicate case values
- C) `switch` cannot use `char` values
- D) `switch` does not require a default case

**Answer:** B

### 44. Which function is used to read a string in C?
- A) `scanf()`
- B) `gets()`
- C) `fscanf()`
- D) `sscanf()`

**Answer:** B

### 45. What is the output of the following program?
```c
#include<stdio.h>
int main() {
char str[20] = “Hello”;
printf(“%s”, str);
return 0;
}
```
- A) Hello
- B) Error
- C) Garbage value
- D) None of the above

**Answer:** A

### 46. What is the output of the following code?
```c
#include<stdio.h>
int main() {
int arr[4] = {1, 2, 3, 4};
printf(“%d”, arr[3]);
return 0;
}
```
- A) 1
- B) 2
- C) 3
- D) 4

**Answer:** D

### 47. How can you declare a pointer to a function in C?
- A) `int (*ptr)();`
- B) `int *ptr();`
- C) `int (*ptr[])();`
- D) `int (*ptr)(int, int);`

**Answer:** D

### 48. What is the difference between `++i` and `i++` in C?
- A) `++i` is post-increment, and `i++` is pre-increment
- B) Both are pre-increments
- C) `++i` increments before, `i++` increments after use
- D) No difference between them

**Answer:** C

### 49. What is the maximum value of an unsigned 8-bit integer?
- A) 127
- B) 255
- C) 511
- D) 1023

**Answer:** B

### 50. What will be the output of the following program?
```c
#include<stdio.h>
int main() {
int a = 5;
printf(“%d”, a == 5 ? 10 : 20);
return 0;
}
```
- A) 5
- B) 10
- C) 20
- D) Error

**Answer:** B
