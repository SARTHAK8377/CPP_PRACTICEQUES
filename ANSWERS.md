ANS1-
```cpp
#include <iostream>
using namespace std;

// Global variable
int globalVar = 10;

int main() {
    // Local variable
    int localVar = 20;

    // Dynamically allocated variable
    int* dynamicVar = new int;
    *dynamicVar = 30;

    // Printing addresses
    cout << "Address of global variable: " << &globalVar << endl;
    cout << "Memory Region: Global / Data Segment" << endl << endl;

    cout << "Address of local variable: " << &localVar << endl;
    cout << "Memory Region: Stack" << endl << endl;

    cout << "Address of dynamically allocated variable: " << dynamicVar << endl;
    cout << "Memory Region: Heap" << endl;

    // Free allocated memory
    delete dynamicVar;

    return 0;
}
```

ANS2-
```cpp
#include <iostream>
using namespace std;

// Function to find square of a number
int square(int x) {
    return x * x;
}

int main() {
    int num = 5;

    // 1. Normal function call
    cout << "Square using normal call: " << square(num) << endl;

    // 2. Function call using function pointer
    int (*fp)(int);   // function pointer declaration
    fp = square;      // assign function address

    cout << "Square using function pointer: " << fp(num) << endl;

    return 0;
}
```

ANS3-
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;      // variable
    int *ptr;        // pointer

    ptr = &x;        // store address of x in pointer

    // Printing required values
    cout << "Value of variable x: " << x << endl;
    cout << "Address of variable x: " << &x << endl;
    cout << "Value stored in pointer ptr: " << ptr << endl;

    return 0;
}
```

ANS4-
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10;      // first variable
    int b;           // third variable (to store copied value)
    int *ptr;        // pointer variable

    ptr = &a;        // pointer stores address of a

    b = *ptr;        // copy value of a into b using dereferencing

    cout << "Value of a: " << a << endl;
    cout << "Value copied into b: " << b << endl;

    return 0;
}
```

ANS5-
```cpp
10
```
ANS6- 
```cpp
1 5
```
ANS7- 
```cpp
20
```
ANS8-
```cpp
2 4
```

ANS9-
```cpp
#include <iostream>
using namespace std;

// Function to swap two numbers using pointers
void swap(int *a, int *b) {
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 5, y = 10;

    cout << "Before swapping: " << x << " " << y << endl;

    swap(&x, &y);   // pass addresses

    cout << "After swapping: " << x << " " << y << endl;

    return 0;
}
```

ANS10-
```cpp
#include <iostream>
using namespace std;

int main() {
    // Create dynamic integer using new
    int *ptr = new int;

    // Modify value through pointer
    *ptr = 50;

    cout << "Value of dynamic integer: " << *ptr << endl;

    // Properly delete allocated memory
    delete ptr;

    return 0;
}
```

ANS11-
```cpp
1 2 4 4
1 4 3 4 5
```

ANS12-
```cpp
10 11
12 12
12 12
```

ANS13- 
```cpp
40 10
```
