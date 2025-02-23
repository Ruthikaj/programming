When you try to **access (dereference) a null pointer** in C, it leads to **undefined behavior (UB)**, which can cause:  

1. **Segmentation Fault (SIGSEGV)** – Most modern OSes prevent access to memory at address `NULL` (0x0), causing the program to crash.  
2. **Crash or Exception** – On some systems, it results in an access violation error.  
3. **Unexpected Behavior** – If not properly handled, it may lead to unpredictable program execution.  

🔹 **Example:**  
```c
#include <stdio.h>

int main() {
    int *ptr = NULL;
    printf("%d", *ptr); // Undefined behavior! Likely a segmentation fault.
    return 0;
}
```
💡 **Best Practice:** Always check for `NULL` before dereferencing.  
```c
if (ptr != NULL) {
    printf("%d", *ptr);
} else {
    printf("Pointer is NULL!");
}
```


### **Behavior of `static` Variable in a Header File**  

If a header file contains a **`static` global variable** and is included in multiple C files, **each file gets its own separate copy** of the variable.  

#### **Example:**
```c
// header.h
#ifndef HEADER_H
#define HEADER_H
#include <stdio.h>

static int count = 0;  // Separate 'count' for each file

void increment() {
    count++;
    printf("Count: %d\n", count);
}

#endif
```

```c
// file1.c
#include "header.h"
int main() {
    increment();  // Increments count of file1.c
    return 0;
}
```

```c
// file2.c
#include "header.h"
int main() {
    increment();  // Increments count of file2.c (different copy)
    return 0;
}
```

#### **Key Takeaways:**
1. **Each C file gets its own independent `count` variable** (not shared).  
2. **Bad practice** – leads to multiple copies and debugging issues.  
3. **Correct approach** – use `extern` in the header and define the variable in a single `.c` file if shared access is needed.  

🔥 **Impressive Fix:**
```c
// header.h
#ifndef HEADER_H
#define HEADER_H
extern int count;
void increment();
#endif

// file1.c
#include "header.h"
int count = 0; // Single definition
void increment() { count++; printf("Count: %d\n", count); }
int main() { increment(); return 0; }

// file2.c
#include "header.h"
int main() { increment(); return 0; }
```
✅ Now, `count` is **shared across all files**, ensuring consistency! 🚀
