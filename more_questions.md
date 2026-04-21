# Creating a Student class with attributes: name, roll number, and marks and performing certain operations.

```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int roll_number;
    float marks;

public:
    // Function to input student details
    void input() {
        std::cout << "Enter name: ";
        std::getline(std::cin, name);
        std::cout << "Enter roll number: ";
        std::cin >> roll_number;
        std::cout << "Enter marks: ";
        std::cin >> marks;
        std::cin.ignore(); // To handle newline after cin
    }

    // Function to display student details
    void display() const {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Roll Number: " << roll_number << std::endl;
        std::cout << "Marks: " << marks << std::endl;
        std::cout << "-------------------" << std::endl;
    }
};

int main() {
    Student s1, s2, s3;

    std::cout << "Enter details for Student 1:" << std::endl;
    s1.input();

    std::cout << "Enter details for Student 2:" << std::endl;
    s2.input();

    std::cout << "Enter details for Student 3:" << std::endl;
    s3.input();

    std::cout << "\nDisplaying student details:" << std::endl;
    s1.display();
    s2.display();
    s3.display();

    return 0;
}
```
INPUT/OUTPUT :-
```
Enter details for Student 1:
Enter name: Alice
Enter roll number: 101
Enter marks: 85
Enter details for Student 2:
Enter name: Bob
Enter roll number: 102
Enter marks: 92
Enter details for Student 3:
Enter name: Charlie
Enter roll number: 103
Enter marks: 78

Displaying student details:
Name: Alice
Roll Number: 101
Marks: 85
-------------------
Name: Bob
Roll Number: 102
Marks: 92
-------------------
Name: Charlie
Roll Number: 103
Marks: 78
-------------------
```


# Creating a BankAccount Class with Constructor and Destructor.

```cpp
#include <iostream>

class BankAccount {
private:
    int account_number;
    double balance;

public:
    // Constructor to initialize account number and balance
    BankAccount(int acc_num, double bal) : account_number(acc_num), balance(bal) {
        std::cout << "Account " << account_number << " created with balance $" << balance << std::endl;
    }

    // Destructor to display a message
    ~BankAccount() {
        std::cout << "Destructor called for account " << account_number << std::endl;
    }
};

// Function to create objects and observe destructor behavior
void createAccounts() {
    BankAccount acc1(12345, 1000.0);
    BankAccount acc2(67890, 2500.0);
    std::cout << "Inside createAccounts function." << std::endl;
    // Objects go out of scope here, destructors will be called
}

int main() {
    std::cout << "Calling createAccounts function:" << std::endl;
    createAccounts();
    std::cout << "Back in main. Program ending." << std::endl;
    return 0;
}
```

INPUT/OUTPUT :-
```
Calling createAccounts function:
Account 12345 created with balance $1000.00
Account 67890 created with balance $2500.00
Inside createAccounts function.
Destructor called for account 67890
Destructor called for account 12345
Back in main. Program ending.
```


# Creating an Employee class with private specifier and validation

```cpp
#include <iostream>
#include <string>

class Employee {
private:
    std::string name;
    double salary;  // Private member

public:
    // Constructor to initialize name and salary
    Employee(std::string emp_name, double emp_salary) : name(emp_name) {
        setSalary(emp_salary);  // Use setter for validation
    }

    // Setter for salary with validation
    void setSalary(double s) {
        if (s >= 0) {
            salary = s;
        } else {
            std::cout << "Error: Salary cannot be negative. Setting to 0." << std::endl;
            salary = 0;
        }
    }

    // Getter for salary
    double getSalary() const {
        return salary;
    }

    // Function to display employee details
    void display() const {
        std::cout << "Name: " << name << std::endl;
        std::cout << "Salary: $" << salary << std::endl;
    }
};

int main() {
    Employee emp1("Alice", 50000.0);
    Employee emp2("Bob", -1000.0);  // Invalid salary, will be set to 0

    std::cout << "Employee 1:" << std::endl;
    emp1.display();

    std::cout << "\nEmployee 2:" << std::endl;
    emp2.display();

    // Demonstrate setter
    emp2.setSalary(45000.0);
    std::cout << "\nAfter updating Employee 2's salary:" << std::endl;
    emp2.display();

    return 0;
}
```

INPUT/OUTPUT :-
```
Employee 1:
Name: Alice
Salary: $50000.00

Employee 2:
Name: Bob
Salary: $0.00

After updating Employee 2's salary:
Name: Bob
Salary: $45000.00
```


# Creating a class Calculator and using method overloading.

```cpp
#include <iostream>

class Calculator {
public:
    // Overloaded add function for two integers
    int add(int a, int b) {
        return a + b;
    }

    // Overloaded add function for two doubles
    double add(double a, double b) {
        return a + b;
    }

    // Overloaded add function for three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }

    // Overloaded add function for three doubles (for completeness)
    double add(double a, double b, double c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;

    // Demonstrate add for two integers
    std::cout << "add(5, 3) = " << calc.add(5, 3) << std::endl;

    // Demonstrate add for two doubles
    std::cout << "add(5.5, 3.2) = " << calc.add(5.5, 3.2) << std::endl;

    // Demonstrate add for three integers
    std::cout << "add(1, 2, 3) = " << calc.add(1, 2, 3) << std::endl;

    // Demonstrate add for three doubles
    std::cout << "add(1.1, 2.2, 3.3) = " << calc.add(1.1, 2.2, 3.3) << std::endl;

    return 0;
}
```

INPUT/OUTPUT :-
```
add(5, 3) = 8
add(5.5, 3.2) = 8.7
add(1, 2, 3) = 6
add(1.1, 2.2, 3.3) = 6.6
```


# Student Class with Dynamic Subjects Array using Struct.

```cpp
#include <iostream>
#include <string>

struct Subject {
    std::string name;
    int marks;
};

class Student {
private:
    int roll;
    std::string name;
    Subject* subjects;
    int n;

public:
    // Constructor: Allocates dynamic memory for n subjects
    Student(int r, std::string nm, int num_subjects) : roll(r), name(nm), n(num_subjects) {
        subjects = new Subject[n];
    }

    // Destructor: Frees dynamic memory for subjects
    ~Student() {
        delete[] subjects;
    }

    // Input function: Inputs details for each subject
    void input() {
        for (int i = 0; i < n; ++i) {
            std::cout << "Enter subject " << (i + 1) << " name: ";
            std::cin >> subjects[i].name;
            std::cout << "Enter marks for " << subjects[i].name << ": ";
            std::cin >> subjects[i].marks;
        }
    }

    // Display function: Shows student and subject details
    void display() const {
        std::cout << "Roll: " << roll << std::endl;
        std::cout << "Name: " << name << std::endl;
        std::cout << "Subjects:" << std::endl;
        for (int i = 0; i < n; ++i) {
            std::cout << "  " << subjects[i].name << ": " << subjects[i].marks << std::endl;
        }
        std::cout << "Total Marks: " << total() << std::endl;
        std::cout << "Grade: " << grade() << std::endl;
        std::cout << "-------------------" << std::endl;
    }

    // Total function: Sums up marks
    int total() const {
        int sum = 0;
        for (int i = 0; i < n; ++i) {
            sum += subjects[i].marks;
        }
        return sum;
    }

    // Grade function: Assigns grade based on total (assuming max marks per subject is 100, total max is 100*n)
    char grade() const {
        int t = total();
        int max_possible = 100 * n;
        double percentage = (static_cast<double>(t) / max_possible) * 100;
        if (percentage >= 90) return 'A';
        else if (percentage >= 80) return 'B';
        else if (percentage >= 70) return 'C';
        else if (percentage >= 60) return 'D';
        else return 'F';
    }

    // Getter for name (used for finding topper)
    std::string getName() const { return name; }
};

int main() {
    int N;
    std::cout << "Enter number of students: ";
    std::cin >> N;

    // Dynamic array of student pointers
    Student** students = new Student*[N];

    for (int i = 0; i < N; ++i) {
        int roll, n_subjects;
        std::string name;
        std::cout << "\nEnter details for Student " << (i + 1) << ":" << std::endl;
        std::cout << "Roll: ";
        std::cin >> roll;
        std::cout << "Name: ";
        std::cin >> name;
        std::cout << "Number of subjects: ";
        std::cin >> n_subjects;

        students[i] = new Student(roll, name, n_subjects);
        students[i]->input();
    }

    // Display all students
    std::cout << "\nDisplaying all students:" << std::endl;
    for (int i = 0; i < N; ++i) {
        students[i]->display();
    }

    // Find topper (student with highest total marks)
    int topper_index = 0;
    int max_total = students[0]->total();
    for (int i = 1; i < N; ++i) {
        if (students[i]->total() > max_total) {
            max_total = students[i]->total();
            topper_index = i;
        }
    }
    std::cout << "Topper: " << students[topper_index]->getName() << " with total marks " << max_total << std::endl;

    // Free memory: Delete each student (destructor handles subjects), then the array
    for (int i = 0; i < N; ++i) {
        delete students[i];
    }
    delete[] students;

    return 0;
}
```

INPUT/OUTPUT :-
```
Enter number of students: 2

Enter details for Student 1:
Roll: 101
Name: Alice
Number of subjects: 2
Enter subject 1 name: Math
Enter marks for Math: 90
Enter subject 2 name: Science
Enter marks for Science: 85

Enter details for Student 2:
Roll: 102
Name: Bob
Number of subjects: 2
Enter subject 1 name: Math
Enter marks for Math: 80
Enter subject 2 name: Science
Enter marks for Science: 95

Displaying all students:
Roll: 101
Name: Alice
Subjects:
  Math: 90
  Science: 85
Total Marks: 175
Grade: A
-------------------
Roll: 102
Name: Bob
Subjects:
  Math: 80
  Science: 95
Total Marks: 175
Grade: A
-------------------
Topper: Alice with total marks 175
```


# PatientQueue Class with Priority Enqueue

```cpp
#include <iostream>
#include <string>

struct Node {
    int id;
    std::string name;
    int severity;
    Node* next;
};

class PatientQueue {
private:
    Node* front;  // Points to the front of the queue (highest priority)

public:
    // Constructor
    PatientQueue() : front(nullptr) {}

    // Destructor: Frees all nodes
    ~PatientQueue() {
        while (front) {
            dequeue();  // Dequeue will handle deletion
        }
    }

    // Enqueue: Inserts based on severity (higher severity first)
    void enqueue(int id, std::string name, int severity) {
        Node* newNode = new Node{id, name, severity, nullptr};

        if (!front || severity > front->severity) {
            // Insert at front if higher severity or empty queue
            newNode->next = front;
            front = newNode;
        } else {
            // Find position to insert (after nodes with higher or equal severity)
            Node* current = front;
            while (current->next && current->next->severity >= severity) {
                current = current->next;
            }
            newNode->next = current->next;
            current->next = newNode;
        }
        std::cout << "Enqueued: " << name << " (ID: " << id << ", Severity: " << severity << ")" << std::endl;
    }

    // Dequeue: Removes and deletes the front node
    void dequeue() {
        if (!front) {
            std::cout << "Queue is empty. Cannot dequeue." << std::endl;
            return;
        }
        Node* temp = front;
        front = front->next;
        std::cout << "Dequeued: " << temp->name << " (ID: " << temp->id << ", Severity: " << temp->severity << ")" << std::endl;
        delete temp;
    }

    // Display: Shows all patients in the queue
    void display() const {
        if (!front) {
            std::cout << "Queue is empty." << std::endl;
            return;
        }
        Node* current = front;
        std::cout << "Patient Queue (from highest to lowest priority):" << std::endl;
        while (current) {
            std::cout << "ID: " << current->id << ", Name: " << current->name << ", Severity: " << current->severity << std::endl;
            current = current->next;
        }
    }
};

int main() {
    PatientQueue queue;

    // Demonstrate enqueue
    queue.enqueue(1, "Alice", 5);
    queue.enqueue(2, "Bob", 3);
    queue.enqueue(3, "Charlie", 7);  // Higher severity, should go to front
    queue.enqueue(4, "Diana", 4);

    std::cout << "\nAfter enqueues:" << std::endl;
    queue.display();

    // Demonstrate dequeue
    std::cout << "\nDequeue operations:" << std::endl;
    queue.dequeue();
    queue.display();

    queue.dequeue();
    queue.display();

    // Add more and dequeue
    queue.enqueue(5, "Eve", 6);
    std::cout << "\nAfter adding Eve:" << std::endl;
    queue.display();

    queue.dequeue();
    queue.display();

    // Destructor will clean up remaining nodes when queue goes out of scope
    return 0;
}
```

INPUT/OUTPUT :-
```
Enqueued: Alice (ID: 1, Severity: 5)
Enqueued: Bob (ID: 2, Severity: 3)
Enqueued: Charlie (ID: 3, Severity: 7)
Enqueued: Diana (ID: 4, Severity: 4)

After enqueues:
Patient Queue (from highest to lowest priority):
ID: 3, Name: Charlie, Severity: 7
ID: 1, Name: Alice, Severity: 5
ID: 4, Name: Diana, Severity: 4
ID: 2, Name: Bob, Severity: 3

Dequeue operations:
Dequeued: Charlie (ID: 3, Severity: 7)
Patient Queue (from highest to lowest priority):
ID: 1, Name: Alice, Severity: 5
ID: 4, Name: Diana, Severity: 4
ID: 2, Name: Bob, Severity: 3

Dequeued: Alice (ID: 1, Severity: 5)
Patient Queue (from highest to lowest priority):
ID: 4, Name: Diana, Severity: 4
ID: 2, Name: Bob, Severity: 3

After adding Eve:
Patient Queue (from highest to lowest priority):
ID: 5, Name: Eve, Severity: 6
ID: 4, Name: Diana, Severity: 4
ID: 2, Name: Bob, Severity: 3

Dequeued: Eve (ID: 5, Severity: 6)
Patient Queue (from highest to lowest priority):
ID: 4, Name: Diana, Severity: 4
ID: 2, Name: Bob, Severity: 3
```


# Library Class with BookNode Linked List

```cpp
#include <iostream>
#include <string>

struct BookNode {
    int id;
    std::string title;
    std::string author;
    bool issued;
    BookNode* next;
};

class Library {
private:
    BookNode* head;

public:
    // Constructor
    Library() : head(nullptr) {}

    // Destructor: Frees all nodes in the linked list
    ~Library() {
        BookNode* current = head;
        while (current) {
            BookNode* temp = current;
            current = current->next;
            delete temp;
        }
    }

    // Add a new book to the end of the list
    void addBook(int id, std::string title, std::string author) {
        BookNode* newNode = new BookNode{id, title, author, false, nullptr};
        if (!head) {
            head = newNode;
        } else {
            BookNode* current = head;
            while (current->next) {
                current = current->next;
            }
            current->next = newNode;
        }
        std::cout << "Book added: " << title << std::endl;
    }

    // Issue a book by ID
    void issueBook(int id) {
        BookNode* current = head;
        while (current) {
            if (current->id == id) {
                if (!current->issued) {
                    current->issued = true;
                    std::cout << "Book issued: " << current->title << std::endl;
                } else {
                    std::cout << "Book already issued: " << current->title << std::endl;
                }
                return;
            }
            current = current->next;
        }
        std::cout << "Book with ID " << id << " not found." << std::endl;
    }

    // Return a book by ID
    void returnBook(int id) {
        BookNode* current = head;
        while (current) {
            if (current->id == id) {
                if (current->issued) {
                    current->issued = false;
                    std::cout << "Book returned: " << current->title << std::endl;
                } else {
                    std::cout << "Book was not issued: " << current->title << std::endl;
                }
                return;
            }
            current = current->next;
        }
        std::cout << "Book with ID " << id << " not found." << std::endl;
    }

    // Search for a book by title
    void searchBook(std::string title) {
        BookNode* current = head;
        while (current) {
            if (current->title == title) {
                std::cout << "Book found - ID: " << current->id << ", Title: " << current->title
                          << ", Author: " << current->author << ", Issued: " << (current->issued ? "Yes" : "No") << std::endl;
                return;
            }
            current = current->next;
        }
        std::cout << "Book with title '" << title << "' not found." << std::endl;
    }

    // Display all books
    void displayAll() {
        if (!head) {
            std::cout << "No books in the library." << std::endl;
            return;
        }
        BookNode* current = head;
        std::cout << "Library Books:" << std::endl;
        while (current) {
            std::cout << "ID: " << current->id << ", Title: " << current->title
                      << ", Author: " << current->author << ", Issued: " << (current->issued ? "Yes" : "No") << std::endl;
            current = current->next;
        }
    }
};

int main() {
    Library lib;

    // Add books
    lib.addBook(1, "1984", "George Orwell");
    lib.addBook(2, "To Kill a Mockingbird", "Harper Lee");
    lib.addBook(3, "The Great Gatsby", "F. Scott Fitzgerald");

    // Display all
    lib.displayAll();

    // Issue and return books
    lib.issueBook(1);
    lib.issueBook(1);  // Try issuing again
    lib.returnBook(1);
    lib.returnBook(1);  // Try returning again

    // Search
    lib.searchBook("1984");
    lib.searchBook("Nonexistent Book");

    // Display again
    lib.displayAll();

    // Destructor will clean up memory
    return 0;
}
```

INPUT/OUTPUT :-
```
Book added: 1984
Book added: To Kill a Mockingbird
Book added: The Great Gatsby
Library Books:
ID: 1, Title: 1984, Author: George Orwell, Issued: No
ID: 2, Title: To Kill a Mockingbird, Author: Harper Lee, Issued: No
ID: 3, Title: The Great Gatsby, Author: F. Scott Fitzgerald, Issued: No
Book issued: 1984
Book already issued: 1984
Book returned: 1984
Book was not issued: 1984
Book found - ID: 1, Title: 1984, Author: George Orwell, Issued: No
Book with title 'Nonexistent Book' not found.
Library Books:
ID: 1, Title: 1984, Author: George Orwell, Issued: No
ID: 2, Title: To Kill a Mockingbird, Author: Harper Lee, Issued: No
ID: 3, Title: The Great Gatsby, Author: F. Scott Fitzgerald, Issued: No
```


# BankAccount Class with Transaction Linked List

```cpp

#include <iostream>
#include <string>

struct Transaction {
    std::string type;  // "Deposit" or "Withdraw"
    double amount;
    std::string date;
    Transaction* next;
};

class BankAccount {
private:
    int accountNo;
    std::string holderName;
    double balance;
    Transaction* historyHead;

public:
    // Constructor
    BankAccount(int accNo, std::string name, double initialBalance = 0.0)
        : accountNo(accNo), holderName(name), balance(initialBalance), historyHead(nullptr) {}

    // Destructor: Frees all transaction nodes
    ~BankAccount() {
        Transaction* current = historyHead;
        while (current) {
            Transaction* temp = current;
            current = current->next;
            delete temp;
        }
    }

    // Deposit money and add to history
    void deposit(double amount, std::string date) {
        balance += amount;
        addTransaction("Deposit", amount, date);
        std::cout << "Deposited $" << amount << " on " << date << ". New balance: $" << balance << std::endl;
    }

    // Withdraw money (if sufficient balance) and add to history
    void withdraw(double amount, std::string date) {
        if (amount > balance) {
            std::cout << "Insufficient balance. Cannot withdraw $" << amount << "." << std::endl;
            return;
        }
        balance -= amount;
        addTransaction("Withdraw", amount, date);
        std::cout << "Withdrew $" << amount << " on " << date << ". New balance: $" << balance << std::endl;
    }

    // Show transaction history
    void showHistory() const {
        if (!historyHead) {
            std::cout << "No transactions for account " << accountNo << "." << std::endl;
            return;
        }
        Transaction* current = historyHead;
        std::cout << "Transaction History for " << holderName << " (Account " << accountNo << "):" << std::endl;
        while (current) {
            std::cout << current->type << " $" << current->amount << " on " << current->date << std::endl;
            current = current->next;
        }
    }

    // Show current balance
    void showBalance() const {
        std::cout << "Account " << accountNo << " (" << holderName << ") Balance: $" << balance << std::endl;
    }

    // Getters for searching
    int getAccountNo() const { return accountNo; }
    std::string getHolderName() const { return holderName; }

private:
    // Helper to add a transaction to the history list
    void addTransaction(std::string type, double amount, std::string date) {
        Transaction* newTrans = new Transaction{type, amount, date, nullptr};
        if (!historyHead) {
            historyHead = newTrans;
        } else {
            Transaction* current = historyHead;
            while (current->next) {
                current = current->next;
            }
            current->next = newTrans;
        }
    }
};

int main() {
    const int NUM_ACCOUNTS = 3;
    BankAccount** accounts = new BankAccount*[NUM_ACCOUNTS];

    // Create accounts
    accounts[0] = new BankAccount(1001, "Alice", 1000.0);
    accounts[1] = new BankAccount(1002, "Bob", 500.0);
    accounts[2] = new BankAccount(1003, "Charlie", 2000.0);

    // Perform operations on accounts
    accounts[0]->deposit(500.0, "2023-10-01");
    accounts[0]->withdraw(200.0, "2023-10-02");
    accounts[1]->withdraw(600.0, "2023-10-03");  // Insufficient balance
    accounts[2]->deposit(1000.0, "2023-10-04");

    // Show balances
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        accounts[i]->showBalance();
    }

    // Show history for one account
    accounts[0]->showHistory();

    // Search for an account by number
    int searchAcc = 1002;
    bool found = false;
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        if (accounts[i]->getAccountNo() == searchAcc) {
            std::cout << "Found account: " << accounts[i]->getHolderName() << std::endl;
            accounts[i]->showHistory();
            found = true;
            break;
        }
    }
    if (!found) {
        std::cout << "Account " << searchAcc << " not found." << std::endl;
    }

    // Free memory: Delete each account (destructor handles transactions), then the array
    for (int i = 0; i < NUM_ACCOUNTS; ++i) {
        delete accounts[i];
    }
    delete[] accounts;

    return 0;
}
```

INPUT/OUTPUT :-
```
Deposited $500.00 on 2023-10-01. New balance: $1500.00
Withdrew $200.00 on 2023-10-02. New balance: $1300.00
Insufficient balance. Cannot withdraw $600.00.
Deposited $1000.00 on 2023-10-04. New balance: $3000.00
Account 1001 (Alice) Balance: $1300.00
Account 1002 (Bob) Balance: $500.00
Account 1003 (Charlie) Balance: $3000.00
Transaction History for Alice (Account 1001):
Deposit $500.00 on 2023-10-01
Withdraw $200.00 on 2023-10-02
Found account: Bob
Transaction History for Bob (Account 1002):
No transactions for account 1002.
```


# Student Class with Dynamic Course Registration

```cpp
#include <iostream>
#include <string>

struct Course {
    std::string courseCode;
    std::string courseName;
    int credits;
};

class Student {
private:
    int roll;
    std::string name;
    Course* registeredCourses;
    int numCourses;
    int capacity;  // For dynamic array growth

public:
    // Constructor: Initializes with empty course list
    Student(int r, std::string nm) : roll(r), name(nm), numCourses(0), capacity(2) {
        registeredCourses = new Course[capacity];
    }

    // Destructor: Frees dynamic course array
    ~Student() {
        delete[] registeredCourses;
    }

    // Register courses: Input multiple courses and add to dynamic array
    void registerCourses() {
        int n;
        std::cout << "Enter number of courses to register for " << name << ": ";
        std::cin >> n;
        for (int i = 0; i < n; ++i) {
            if (numCourses == capacity) {
                // Grow array
                capacity *= 2;
                Course* newArray = new Course[capacity];
                for (int j = 0; j < numCourses; ++j) {
                    newArray[j] = registeredCourses[j];
                }
                delete[] registeredCourses;
                registeredCourses = newArray;
            }
            std::cout << "Enter course code: ";
            std::cin >> registeredCourses[numCourses].courseCode;
            std::cout << "Enter course name: ";
            std::cin.ignore();  // Handle newline
            std::getline(std::cin, registeredCourses[numCourses].courseName);
            std::cout << "Enter credits: ";
            std::cin >> registeredCourses[numCourses].credits;
            ++numCourses;
        }
    }

    // Drop a course by code
    void dropCourse(std::string code) {
        for (int i = 0; i < numCourses; ++i) {
            if (registeredCourses[i].courseCode == code) {
                // Shift elements left
                for (int j = i; j < numCourses - 1; ++j) {
                    registeredCourses[j] = registeredCourses[j + 1];
                }
                --numCourses;
                std::cout << "Dropped course: " << code << std::endl;
                return;
            }
        }
        std::cout << "Course " << code << " not found for " << name << std::endl;
    }

    // Show all registered courses
    void showCourses() const {
        std::cout << name << "'s courses:" << std::endl;
        if (numCourses == 0) {
            std::cout << "  No courses registered." << std::endl;
            return;
        }
        for (int i = 0; i < numCourses; ++i) {
            std::cout << "  " << registeredCourses[i].courseCode << " - " << registeredCourses[i].courseName
                      << " (" << registeredCourses[i].credits << " credits)" << std::endl;
        }
    }

    // Total credits
    int totalCredits() const {
        int total = 0;
        for (int i = 0; i < numCourses; ++i) {
            total += registeredCourses[i].credits;
        }
        return total;
    }

    // Check if student is registered in a course
    bool isRegisteredIn(std::string code) const {
        for (int i = 0; i < numCourses; ++i) {
            if (registeredCourses[i].courseCode == code) return true;
        }
        return false;
    }

    // Getters
    int getRoll() const { return roll; }
    std::string getName() const { return name; }
};

int main() {
    int N;
    std::cout << "Enter number of students: ";
    std::cin >> N;

    // Dynamic array of student pointers
    Student** students = new Student*[N];

    for (int i = 0; i < N; ++i) {
        int roll;
        std::string name;
        std::cout << "\nEnter roll and name for Student " << (i + 1) << ": ";
        std::cin >> roll >> name;
        students[i] = new Student(roll, name);
        students[i]->registerCourses();
    }

    // Display all students
    std::cout << "\nAll Students:" << std::endl;
    for (int i = 0; i < N; ++i) {
        students[i]->showCourses();
        std::cout << "Total Credits: " << students[i]->totalCredits() << std::endl;
        std::cout << "-------------------" << std::endl;
    }

    // Print students registered in a given course
    std::string courseCode;
    std::cout << "Enter course code to list registered students: ";
    std::cin >> courseCode;
    std::cout << "Students registered in " << courseCode << ":" << std::endl;
    bool found = false;
    for (int i = 0; i < N; ++i) {
        if (students[i]->isRegisteredIn(courseCode)) {
            std::cout << "  " << students[i]->getName() << " (Roll: " << students[i]->getRoll() << ")" << std::endl;
            found = true;
        }
    }
    if (!found) {
        std::cout << "  No students registered." << std::endl;
    }

    // Free memory
    for (int i = 0; i < N; ++i) {
        delete students[i];
    }
    delete[] students;

    return 0;
}
```

INPUT/OUTPUT :-
```
Enter number of students: Enter roll and name for Student 1: Enter number of courses to register for Alice: Enter course code: Enter course name: Enter credits: Enter course code: Enter course name: Enter credits: Enter roll and name for Student 2: Enter number of courses to register for Bob: Enter course code: Enter course name: Enter credits: 
All Students:
Alice's courses:
  CS101 - Intro to CS (3 credits)
  MATH101 - Calculus (4 credits)
Total Credits: 7
-------------------
Bob's courses:
  CS101 - Intro to CS (3 credits)
Total Credits: 3
-------------------
Enter course code to list registered students: Students registered in CS101:
  Alice (Roll: 1)
  Bob (Roll: 2)
```


# Directory Tree Implementation

```cpp
#include <iostream>
#include <vector>
#include <sstream>
#include <string>

struct DirNode {
    std::string name;
    bool isFile;
    DirNode* child;
    DirNode* sibling;
};

class DirectoryTree {
private:
    DirNode* root;

    std::vector<std::string> splitPath(std::string path) {
        std::vector<std::string> parts;
        std::stringstream ss(path);
        std::string token;
        while (std::getline(ss, token, '/')) {
            if (!token.empty()) parts.push_back(token);
        }
        return parts;
    }

    DirNode* findNode(std::string path) {
        auto parts = splitPath(path);
        DirNode* current = root;
        for (auto& part : parts) {
            DirNode* child = current->child;
            while (child) {
                if (child->name == part) {
                    current = child;
                    break;
                }
                child = child->sibling;
            }
            if (!child) return nullptr;
        }
        return current;
    }

    void deleteSubtree(DirNode* node) {
        if (!node) return;
        deleteSubtree(node->child);
        deleteSubtree(node->sibling);
        delete node;
    }

public:
    DirectoryTree() {
        root = new DirNode{"/", false, nullptr, nullptr};
    }

    ~DirectoryTree() {
        deleteSubtree(root);
    }

    void createFolder(std::string path) {
        auto parts = splitPath(path);
        DirNode* current = root;
        for (auto& part : parts) {
            DirNode* child = current->child;
            DirNode* prev = nullptr;
            while (child) {
                if (child->name == part) {
                    if (child->isFile) {
                        std::cout << "Cannot create folder: file exists at " << part << std::endl;
                        return;
                    }
                    current = child;
                    break;
                }
                prev = child;
                child = child->sibling;
            }
            if (!child) {
                DirNode* newNode = new DirNode{part, false, nullptr, nullptr};
                if (prev) {
                    prev->sibling = newNode;
                } else {
                    current->child = newNode;
                }
                current = newNode;
            }
        }
    }

    void createFile(std::string path) {
        auto parts = splitPath(path);
        if (parts.empty()) {
            std::cout << "Invalid path for file" << std::endl;
            return;
        }
        std::string fileName = parts.back();
        parts.pop_back();
        std::string dirPath = "/";
        for (size_t i = 0; i < parts.size(); ++i) {
            dirPath += parts[i];
            if (i < parts.size() - 1) dirPath += "/";
        }
        DirNode* parent = findNode(dirPath);
        if (!parent || parent->isFile) {
            std::cout << "Invalid parent path" << std::endl;
            return;
        }
        DirNode* child = parent->child;
        while (child) {
            if (child->name == fileName) {
                if (!child->isFile) {
                    std::cout << "Folder exists with that name" << std::endl;
                } else {
                    std::cout << "File already exists" << std::endl;
                }
                return;
            }
            child = child->sibling;
        }
        DirNode* newFile = new DirNode{fileName, true, nullptr, nullptr};
        if (!parent->child) {
            parent->child = newFile;
        } else {
            child = parent->child;
            while (child->sibling) child = child->sibling;
            child->sibling = newFile;
        }
    }

    void list(std::string path) {
        DirNode* node = findNode(path);
        if (!node) {
            std::cout << "Path not found" << std::endl;
            return;
        }
        if (node->isFile) {
            std::cout << node->name << " (file)" << std::endl;
            return;
        }
        std::cout << "Contents of " << path << ":" << std::endl;
        DirNode* child = node->child;
        while (child) {
            std::cout << (child->isFile ? "File: " : "Folder: ") << child->name << std::endl;
            child = child->sibling;
        }
    }

    void deleteNode(std::string path) {
        auto parts = splitPath(path);
        if (parts.empty()) {
            std::cout << "Cannot delete root" << std::endl;
            return;
        }
        std::string name = parts.back();
        parts.pop_back();
        std::string parentPath = "/";
        for (size_t i = 0; i < parts.size(); ++i) {
            parentPath += parts[i];
            if (i < parts.size() - 1) parentPath += "/";
        }
        DirNode* parent = findNode(parentPath);
        if (!parent || parent->isFile) {
            std::cout << "Invalid parent path" << std::endl;
            return;
        }
        DirNode* child = parent->child;
        DirNode* prev = nullptr;
        while (child) {
            if (child->name == name) {
                if (prev) {
                    prev->sibling = child->sibling;
                } else {
                    parent->child = child->sibling;
                }
                deleteSubtree(child);
                std::cout << "Deleted " << path << std::endl;
                return;
            }
            prev = child;
            child = child->sibling;
        }
        std::cout << "Node not found" << std::endl;
    }
};

int main() {
    DirectoryTree dt;

    // Sample operations
    dt.createFolder("/a");
    dt.createFolder("/a/b");
    dt.createFile("/a/b/file1.txt");
    dt.createFile("/a/file2.txt");
    dt.list("/a");
    dt.list("/a/b");
    dt.deleteNode("/a/b/file1.txt");
    dt.list("/a/b");

    return 0;
}
```

INPUT/OUTPUT :-
```
Contents of /a:
Folder: b
File: file2.txt
Contents of /a/b:
File: file1.txt
Deleted /a/b/file1.txt
Contents of /a/b:
```
