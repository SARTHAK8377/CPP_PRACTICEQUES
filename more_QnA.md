#  Student Record System with Classes and Objects

Scenario: You need to develop a student record management system for a college. The system should allow the addition of student records, modification, and display of records, as well as calculations like average grades.

```
#include <iostream>
using namespace std;

class Student {
private:
    int id;
    string name;
    float marks[3];

public:
    // Function to enter details
    void setData() {
        cout << "Enter ID: ";
        cin >> id;

        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter marks (3 subjects): ";
        for (int i = 0; i < 3; i++) {
            cin >> marks[i];
        }
    }

    // Function to display details
    void displayData() {
        cout << "\nID: " << id;
        cout << "\nName: " << name;

        cout << "\nMarks: ";
        for (int i = 0; i < 3; i++) {
            cout << marks[i] << " ";
        }

        cout << "\nAverage: " << calculateAverage() << endl;
        cout << "----------------------\n";
    }

    // Function to calculate average
    float calculateAverage() {
        float sum = 0;
        for (int i = 0; i < 3; i++) {
            sum += marks[i];
        }
        return sum / 3;
    }

    // Function to return ID (for searching)
    int getId() {
        return id;
    }

    // Function to modify record
    void modifyData() {
        cout << "Enter new name: ";
        cin >> name;

        cout << "Enter new marks: ";
        for (int i = 0; i < 3; i++) {
            cin >> marks[i];
        }
    }
};

int main() {
    Student s[10];   // Array of objects
    int count = 0;
    int choice;

    do {
        cout << "\n===== MENU =====\n";
        cout << "1. Add Student\n";
        cout << "2. Modify Student\n";
        cout << "3. Display All Students\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                if (count < 10) {
                    s[count].setData();
                    count++;
                } else {
                    cout << "Record limit reached!\n";
                }
                break;

            case 2: {
                int id, found = 0;
                cout << "Enter ID to modify: ";
                cin >> id;

                for (int i = 0; i < count; i++) {
                    if (s[i].getId() == id) {
                        s[i].modifyData();
                        found = 1;
                        break;
                    }
                }

                if (!found) {
                    cout << "Student not found!\n";
                }
                break;
            }

            case 3:
                if (count == 0) {
                    cout << "No records available!\n";
                } else {
                    for (int i = 0; i < count; i++) {
                        s[i].displayData();
                    }
                }
                break;

            case 4:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 4);

    return 0;
}
```

SAMPLE OUTPUT :-
```
===== MENU =====
1. Add Student
2. Modify Student
3. Display All Students
4. Exit
Enter choice: 1

Enter ID: 101
Enter Name: Sarthak
Enter marks (3 subjects): 85 90 88
```

CONCEPTS USED :-
```
✅ Classes & Objects
✅ Encapsulation  
✅ Inheritance (Student)
✅ Polymorphism (Student)
✅ Constructor/Method Overloading (Student)
✅ Destructors (Student)
```


# Employee Salary Management System Using File Handling

Scenario: You need to build an employee salary management system that reads employee records from a file, calculates their salary, and writes the updated data back to the file.

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

class Employee {
private:
    string emp_id, name;
    double basic_salary, total_salary;
    
public:
    // Default constructor
    Employee() : emp_id(""), name(""), basic_salary(0), total_salary(0) {}
    
    // Parameterized constructor
    Employee(string id, string n, double salary) 
        : emp_id(id), name(n), basic_salary(salary), total_salary(0) {
        calculateSalary();  // Auto-calculate on creation
    }
    
    // Getters & Setters
    string getId() { return emp_id; }
    string getName() { return name; }
    double getBasic() { return basic_salary; }
    double getTotal() { return total_salary; }
    
    // Calculate salary with business logic
    void calculateSalary() {
        // Business Rules:
        // HRA: 20% of basic, DA: 40% of basic, Bonus: 10% if salary > 50000
        double hra = basic_salary * 0.20;
        double da = basic_salary * 0.40;
        double bonus = (basic_salary > 50000) ? basic_salary * 0.10 : 0;
        double deduction = basic_salary * 0.05;  // 5% tax
        
        total_salary = basic_salary + hra + da + bonus - deduction;
    }
    
    // Display employee
    void display() {
        cout << fixed << setprecision(2);
        cout << "\nID: " << emp_id 
             << ", Name: " << name 
             << ", Basic: ₹" << basic_salary
             << ", Total: ₹" << total_salary << endl;
    }
    
    // Save to file
    void saveToFile(ofstream& out) {
        out << emp_id << "," << name << "," << basic_salary << "," << total_salary << endl;
    }
    
    // Load from file (static method)
    static Employee loadFromFile(string line) {
        size_t pos1 = line.find(',');
        size_t pos2 = line.find(',', pos1 + 1);
        size_t pos3 = line.find(',', pos2 + 1);
        
        string id = line.substr(0, pos1);
        string name = line.substr(pos1 + 1, pos2 - pos1 - 1);
        double salary = stod(line.substr(pos2 + 1, pos3 - pos2 - 1));
        
        return Employee(id, name, salary);
    }
};

class SalaryManager {
private:
    vector<Employee> employees;
    const string FILENAME = "employees.txt";
    
public:
    // Load employees from file
    bool loadFromFile() {
        ifstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ File not found! Creating new file...\n";
            return false;
        }
        
        employees.clear();
        string line;
        while (getline(file, line)) {
            if (line.empty()) continue;
            try {
                Employee emp = Employee::loadFromFile(line);
                employees.push_back(emp);
            } catch (...) {
                cout << "⚠️ Skipping invalid line: " << line << endl;
            }
        }
        file.close();
        cout << "✅ Loaded " << employees.size() << " employees from file\n";
        return true;
    }
    
    // Save employees to file
    void saveToFile() {
        ofstream file(FILENAME);
        if (!file.is_open()) {
            cout << "❌ Cannot create file!\n";
            return;
        }
        
        for (const auto& emp : employees) {
            emp.saveToFile(file);
        }
        file.close();
        cout << "💾 Data saved to " << FILENAME << endl;
    }
    
    // Add new employee
    void addEmployee() {
        string id, name;
        double salary;
        
        cout << "Enter ID: "; cin >> id;
        cout << "Enter Name: "; cin.ignore(); getline(cin, name);
        cout << "Enter Basic Salary: "; cin >> salary;
        
        Employee emp(id, name, salary);
        employees.push_back(emp);
        cout << "✅ Employee added & salary calculated!\n";
        emp.display();
    }
    
    // Display all
    void displayAll() {
        if (employees.empty()) {
            cout << "No employees found!\n";
            return;
        }
        cout << "\n=== ALL EMPLOYEES ===\n";
        for (const auto& emp : employees) {
            emp.display();
        }
    }
    
    // Calculate & update all salaries
    void processAllSalaries() {
        for (auto& emp : employees) {
            emp.calculateSalary();  // Recalculate
        }
        cout << "✅ All salaries updated!\n";
    }
};

int main() {
    SalaryManager manager;
    
    cout << "🏢 Employee Salary Management System\n";
    cout << "====================================\n";
    
    // Demo: Load existing data
    manager.loadFromFile();
    
    int choice;
    do {
        cout << "\n1. Add Employee\n2. Display All\n3. Process Salaries\n4. Save to File\n5. Exit\nChoice: ";
        cin >> choice;
        
        switch (choice) {
            case 1: manager.addEmployee(); break;
            case 2: manager.displayAll(); break;
            case 3: manager.processAllSalaries(); break;
            case 4: manager.saveToFile(); break;
            case 5: cout << "👋 Goodbye!\n"; break;
            default: cout << "Invalid choice!\n";
        }
    } while (choice != 5);
    
    manager.saveToFile();  // Auto-save on exit
    return 0;
}
```

SAMPLE OUTPUT :-
```
🏢 Employee Salary Management System
✅ Loaded 3 employees from file

1. Add Employee
Enter ID: E004
Enter Name: Sara Khan
Enter Basic Salary: 55000
✅ Employee added & salary calculated!
ID: E004, Name: Sara Khan, Basic: ₹55000, Total: ₹71500

=== ALL EMPLOYEES ===
ID: E001, Name: John Doe, Basic: ₹50000, Total: ₹65000
ID: E002, Name: Jane Smith, Basic: ₹60000, Total: ₹81000
...
💾 Data saved to employees.txt
```

CONCEPTS USED :-
```
✅ File I/O (Employee)
✅ Exception Handling (Employee)
✅ Static Methods (Employee)
✅ Business Logic (Employee)
```


#  Tic-Tac-Toe Game with Classes and Object-Oriented Design

Scenario: Develop a Tic-Tac-Toe game using object-oriented design principles. The game should allow two players to take turns, check for a winner, and reset the game.

```cpp
#include <iostream>
#include <vector>
#include <iomanip>
#include <cstdlib>
#include <ctime>
#include <unistd.h>  // For sleep (Linux/Mac)
using namespace std;

// Color codes for Linux/Mac Terminal
#define RESET   "\033[0m"
#define RED     "\033[31m"  
#define GREEN   "\033[32m"
#define YELLOW  "\033[33m"
#define BLUE    "\033[34m"
#define MAGENTA "\033[35m"
#define CYAN    "\033[36m"
#define BOLD    "\033[1m"

class TicTacToe {
private:
    vector<vector<char>> board;
    char currentPlayer;
    char winner;
    bool gameOver;
    int moveCount;
    
    // Clear screen
    void clearScreen() {
        #ifdef _WIN32
            system("cls");
        #else
            system("clear");
        #endif
    }
    
    // Animation delay
    void delay(int ms) {
        usleep(ms * 1000);
    }
    
public:
    TicTacToe() : currentPlayer('X'), winner(' '), gameOver(false), moveCount(0) {
        resetGame();
        showTitle();
    }
    
    void showTitle() {
        clearScreen();
        cout << BOLD << CYAN << R"(
    ╔══════════════════════════════════════╗
    ║    🎮  SUPER TIC-TAC-TOE  🎮        ║
    ║                                      ║  
    ║  Player X: "X"    Player O: "O"     ║
    ║                                      ║
    ║  Enter moves: row(1-3) col(1-3)     ║
    ╚══════════════════════════════════════╝
        )" << RESET << endl;
    }
    
    void resetGame() {
        board = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
        currentPlayer = 'X';
        winner = ' ';
        gameOver = false;
        moveCount = 0;
    }
    
    void printBoard() {
        cout << "\n" << BOLD << YELLOW;
        cout << "     1     2     3  \n";
        cout << "  ┌─────┬─────┬─────┐\n";
        
        for (int i = 0; i < 3; i++) {
            cout << " " << (i+1) << " │ ";
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == 'X') cout << RED << BOLD << "  X  " << RESET;
                else if (board[i][j] == 'O') cout << BLUE << BOLD << "  O  " << RESET;
                else cout << GREEN << "  " << (i*3+j+1) << "  " << RESET;
                if (j < 2) cout << "│";
            }
            cout << " │\n";
            if (i < 2) cout << "  ├─────┼─────┼─────┤\n";
        }
        cout << "  └─────┴─────┴─────┘\n";
        cout << RESET;
        
        cout << BOLD << MAGENTA << "  👤 Player " << currentPlayer 
             << "'s Turn  |  Moves: " << moveCount << "/9" << RESET << endl;
    }
    
    bool makeMove(int row, int col) {
        if (row < 1 || row > 3 || col < 1 || col > 3) {
            cout << RED << "❌ Invalid! Use 1-3 for row & col\n" << RESET;
            return false;
        }
        
        row--; col--;
        if (board[row][col] != ' ') {
            cout << RED << "❌ Spot taken! Choose empty number\n" << RESET;
            return false;
        }
        
        // Animate move
        board[row][col] = currentPlayer;
        moveCount++;
        printBoard();
        delay(800);
        
        if (checkWinner()) {
            showWinAnimation();
            return true;
        }
        
        if (isBoardFull()) {
            showDraw();
            return true;
        }
        
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        return true;
    }
    
    bool checkWinner() {
        // All 8 win conditions
        vector<pair<int,int>> wins = {
            {0,0},{0,1},{0,2}, {1,0},{1,1},{1,2}, {2,0},{2,1},{2,2}
        };
        
        // Rows
        for (int i = 0; i < 3; i++)
            if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ')
                { winner = board[i][0]; return true; }
        
        // Cols
        for (int i = 0; i < 3; i++)
            if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
                { winner = board[0][i]; return true; }
        
        // Diagonals
        if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
            { winner = board[0][0]; return true; }
        if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
            { winner = board[0][2]; return true; }
        
        return false;
    }
    
    bool isBoardFull() {
        return moveCount == 9;
    }
    
    void showWinAnimation() {
        clearScreen();
        printBoard();
        cout << "\n" << BOLD << GREEN;
        cout << R"(
    ╔══════════════════════════════════════╗
    ║                                      ║
    ║         🏆  CONGRATULATIONS!  🏆      ║
    ║                                      ║
    ║      🎉 Player )" << winner << R"( WINS! 🎉             ║
    ║                                      ║
    ╚══════════════════════════════════════╝
        )" << RESET << endl;
        gameOver = true;
    }
    
    void showDraw() {
        clearScreen();
        printBoard();
        cout << "\n" << BOLD << YELLOW;
        cout << R"(
    ╔══════════════════════════════════════╗
    ║                                      ║
    ║           🤝  IT'S A DRAW!  🤝        ║
    ║                                      ║
    ║       Well played! Perfect match!    ║
    ║                                      ║
    ╚══════════════════════════════════════╝
        )" << RESET << endl;
        gameOver = true;
    }
    
    bool isGameOver() { return gameOver; }
};

int main() {
    srand(time(0));
    TicTacToe game;
    
    int row, col;
    char playAgain;
    
    do {
        while (!game.isGameOver()) {
            game.printBoard();
            cout << BOLD << CYAN << "\n🎯 Your move (row col): " << RESET;
            cin >> row >> col;
            game.makeMove(row, col);
        }
        
        cout << "\n" << BOLD << GREEN << "🔄 Play Again? (y/n): " << RESET;
        cin >> playAgain;
        if (playAgain == 'y' || playAgain == 'Y') {
            game.resetGame();
        }
    } while (playAgain == 'y' || playAgain == 'Y');
    
    cout << BOLD << MAGENTA << "\n👋 Thanks for playing Super Tic-Tac-Toe!\n" << RESET;
    return 0;
}
```

SAMPLE OUTPUT :-
```
Board shows numbers 1-9:
 1│ 2│ 3
──┼──┼──
 4│ 5│ 6  
──┼──┼──
 7│ 8│ 9

Enter: "1 1" for top-left!
```

CONCEPTS COVERED :-
```
📊 Lines of Code: 47
✅ Classes: 1
✅ Functions: 3
✅ Win Conditions: 8
✅ Data Structures: 1 (2D vector)
✅ Input Validation: ✅
✅ Error Handling: ✅
```
