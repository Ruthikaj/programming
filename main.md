### **📌 Storage Classes in C**
C has **four storage classes** that define the **scope, lifetime, and linkage** of variables:  

1️⃣ **`auto` (Automatic Storage)**  
   - Default for local variables.  
   - Stored in the **stack** and exists only within the function.  
   - Example:  
     ```c
     void func() {
         auto int x = 10; // x is destroyed after function exits
     }
     ```

2️⃣ **`register` (CPU Register Storage)**  
   - Hints the compiler to store the variable in **CPU registers** (faster access).  
   - Cannot get the address using `&`.  
   - Example:  
     ```c
     register int count = 0;
     ```

3️⃣ **`static` (Static Storage)**  
   - Retains value **between function calls** (stored in **data segment**).  
   - Scope remains local, but lifetime extends throughout the program.  
   - Example:  
     ```c
     void func() {
         static int count = 0; // Retains value across calls
         count++;
         printf("%d ", count);
     }
     ```

4️⃣ **`extern` (Global Variable Declaration)**  
   - Used for **global variable access** across multiple files.  
   - Defined in one `.c` file and declared in others using `extern`.  
   - Example:  
     ```c
     // file1.c
     int x = 10; // Definition
     ```

     ```c
     // file2.c
     extern int x; // Declaration
     ```

---

### **📌 `volatile` Keyword**
🔹 **Prevents compiler optimizations on a variable** – ensures every access reads from memory.  
🔹 Used when **variable value can change unexpectedly**, like in **hardware registers, shared memory, or interrupts**.  

✅ **Example:**  
```c
volatile int sensor_value;
while(sensor_value != 100) {
    // Compiler won't optimize this loop away
}
```
💡 Without `volatile`, the compiler might assume `sensor_value` **never changes**, leading to an **infinite loop**.

---

### **📌 `const` Keyword**
🔹 Declares **read-only variables**.  
🔹 Ensures the **value cannot be modified** after initialization.  

✅ **Example:**  
```c
const int max_value = 100;
max_value = 200; // ❌ Error: Cannot modify 'const' variable
```

---

### **📌 `volatile` + `const` Usage in Real Life (Reading Data from USB/Pen Drives)**
🔹 **Example:** Reading a memory-mapped hardware register (e.g., USB controller).  
```c
const volatile int *usb_data = (int *) 0x4000;  // Address of hardware register
int read_value = *usb_data;  // Always fetch fresh value
```
- **`volatile`**: Ensures the latest value is always read from memory.  
- **`const`**: Prevents accidental modification.  

---

### **📌 C Program Compilation Stages**
C compilation happens in **four stages**:  

1️⃣ **Preprocessing (`.i` file)** – Handles `#include`, `#define`, macros, removes comments.  
2️⃣ **Compilation (`.s` file)** – Converts C code into **assembly language**.  
3️⃣ **Assembly (`.o` file)** – Converts assembly into **machine code**.  
4️⃣ **Linking (Executable file)** – Links multiple `.o` files and libraries.  

✅ **Command:**
```sh
gcc -E file.c -o file.i  # Preprocessing
gcc -S file.i -o file.s  # Compilation
gcc -c file.s -o file.o  # Assembly
gcc file.o -o file       # Linking (creates executable)
```

---

### **📌 `struct` vs `union`**
| Feature  | `struct` | `union` |
|----------|---------|---------|
| **Memory** | Allocates memory for all members | Allocates memory for the largest member |
| **Size** | Sum of all members' sizes (plus padding) | Size of the largest member |
| **Access** | All members can hold values simultaneously | Only **one member** can hold a value at a time |
| **Use Case** | Data grouping (e.g., student record) | Memory-efficient storage (e.g., variant data types) |

✅ **Example:**
```c
struct Data {
    int a;
    float b;
    char c;
}; // Size: 4 + 4 + 1 (padding applied)

union Data {
    int a;
    float b;
    char c;
}; // Size: max(4,4,1) = 4
```

---

### **📌 Pass By Value vs Pass By Reference for Pointers**
| Type | Description | Example |
|------|------------|---------|
| **Pass By Value** | Copies the pointer, does NOT modify original | `func(int *ptr)` |
| **Pass By Reference** | Modifies the actual pointer | `func(int **ptr)` |

✅ **Example:**
```c
#include <stdio.h>

void byValue(int *p) {
    p = NULL; // Only local copy of 'p' is modified
}

void byReference(int **p) {
    *p = NULL; // Actual pointer in caller is modified
}

int main() {
    int x = 10, *ptr = &x;
    byValue(ptr);
    printf("%p\n", ptr); // Not NULL (unchanged)

    byReference(&ptr);
    printf("%p\n", ptr); // NULL (modified)
}
```

---

### **📌 Calculate the Size of `struct` Without Using `sizeof()` (Pointer Arithmetic)**
🔹 **Trick:** Use pointer arithmetic to find the byte difference between consecutive elements in an array.

✅ **Example:**
```c
#include <stdio.h>

struct Data {
    int a;
    char b;
    double c;
};

int main() {
    struct Data arr[2];  
    printf("Size of struct: %ld\n", (char *)&arr[1] - (char *)&arr[0]);
    return 0;
}
```
**Explanation:**  
- `arr[0]` and `arr[1]` are adjacent in memory.  
- `(char *)` ensures pointer arithmetic works at the byte level.  
- **Output:** Prints actual size of `struct Data`.  

### **1. Difference between `getch()` and `getche()` in C**  
| Feature  | `getch()` | `getche()` |
|----------|----------|------------|
| Echo on Screen | No  | Yes |
| Waits for Input | Yes | Yes |
| Returns Character | Yes | Yes |
| Use Case | Used when we don't want input to be displayed | Used when we need input visibility |

#### **Example**  
```c
#include <stdio.h>
#include <conio.h>

int main() {
    char ch1, ch2;
    printf("Enter a character using getch(): ");
    ch1 = getch();
    printf("\nYou entered: %c\n", ch1);

    printf("Enter a character using getche(): ");
    ch2 = getche();
    printf("\nYou entered: %c\n", ch2);

    return 0;
}
```
✅ `getch()` is useful for password input, while `getche()` is useful for interactive prompts.

---

### **2. Difference between `abs()` and `fabs()` in C**  
| Function  | `abs()` | `fabs()` |
|-----------|--------|----------|
| Header File | `<stdlib.h>` | `<math.h>` |
| Return Type | `int` | `double` |
| Input Type | `int` | `float/double` |
| Purpose | Absolute value of integers | Absolute value of floating points |

#### **Example**  
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int main() {
    int num1 = -10;
    double num2 = -10.5;

    printf("abs(-10) = %d\n", abs(num1));
    printf("fabs(-10.5) = %.2f\n", fabs(num2));

    return 0;
}
```
✅ `abs()` works with integers, while `fabs()` is used for floating-point numbers.

---

### **3. Structure Padding and Packing**  

#### **Padding**  
- **Definition:** Compiler automatically inserts extra bytes between structure members to align them efficiently in memory.
- **Who does it?** → **Compiler**
- **Why?** → To improve CPU performance by ensuring data is accessed efficiently.

#### **Example (With Padding)**  
```c
#include <stdio.h>

struct Padded {
    char a;     // 1 byte
    int b;      // 4 bytes (alignment adds 3 extra bytes after 'a')
    char c;     // 1 byte
};

int main() {
    printf("Size of struct: %lu bytes\n", sizeof(struct Padded));
    return 0;
}
```
🔹 Size will be **8 bytes** (due to padding).

---

#### **Packing**  
- **Definition:** Prevents compiler from adding padding, making the structure more memory-efficient.
- **Who does it?** → **Compiler (with directives)**
- **Why?** → Used when memory is critical (e.g., embedded systems, file formats).

#### **Example (With Packing)**  
```c
#include <stdio.h>
#pragma pack(1)  // Disable padding

struct Packed {
    char a;
    int b;
    char c;
};

int main() {
    printf("Size of packed struct: %lu bytes\n", sizeof(struct Packed));
    return 0;
}
```
🔹 Size will be **6 bytes** (no padding).
