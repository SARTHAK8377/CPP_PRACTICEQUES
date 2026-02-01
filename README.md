# CPP_PRACTICEQUES
Q1 
Write a C++ program that:
Declares one global variable
Declares one local variable inside main()
Dynamically allocates one integer using new
Print the addresses of all three and identify which memory region each belongs to.

Q2
Write a function square(int) and call it:
Normally
Using a function pointer

Q3
Write a program to print:
Value of a variable
Address of the variable
Value stored in the pointer

Q4
Write a program where a pointer stores the address of another variable and copies its value into a third variable using dereferencing.

Q5
What will be the output:
A)
int x = 5;
int *p = &x;
*p = 10;
cout << x;

B)
int a = 1, b = 2;
int *p = &a;
p = &b;
*p = 5;
cout << a << " " << b;

C)
int x = 10;
int *p = &x;
int **pp = &p;
**pp = 20;
cout << x;

D)
nt a[5] = {2,4,6,8,10};
int *p = a;
cout << *p++ << " ";
cout << *p;


Q6
Write a program to swap two numbers using pointers

Q7
Implement a simple dynamic integer variable that:
Is created using new
Modified through a pointer
Properly deleted

Q8
int a[] = {1,2,3,4,5};
int *p = a;
cout << *p++ << " ";
cout << (*p)++ << " ";
cout << ++*p << " ";
cout << *p << "\n";
for(int i=0;i<5;i++) cout << a[i] << " ";

Q9
int x=10;
int *p=&x;
cout << (*p)++ << " " << x << "\n";
cout << ++(*p) << " " << x << "\n";
cout << *p++ << " " << x << "\n";

Q10
int a[] = {10,20,30,40,50};
int *p = a + 1;
cout << *(p+2) << " " << *(p-1) << "\n";
