#  Student Record System with Classes and Objects

Scenario: You need to develop a student record management system for a college. The system should allow the addition of student records, modification, and display of records, as well as calculations like average grades.

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Student {
private:
    int roll_number;
    string name;
    float marks[3];
public:
    // Default Constructor
    Student() {
        roll_number = 0;
        name = "Unknown";
        for(int i = 0; i < 3; i++) marks[i] = 0;
    }
    Student(int r, string n, float m[]) {
        roll_number = r;
        name = n;
        for(int i = 0; i < 3; i++) marks[i] = m[i];
    }
    Student(int r) {
        roll_number = r;
        name = "Not Assigned";
        for(int i = 0; i < 3; i++) marks[i] = 0;
    }
    // Destructor
    ~Student() {
    }
    // Add Student (Method Overloading)
    void addStudent(int r, string n, float m[]) {
        roll_number = r;
        name = n;
        for(int i = 0; i < 3; i++) marks[i] = m[i];
    }
    void addStudent(int r) {
        roll_number = r;
        name = "Temporary";
        for(int i = 0; i < 3; i++) marks[i] = 0;
    }
    // Modify Student
    void modifyStudent(string newName, float newMarks[]) {
        name = newName;
        for(int i = 0; i < 3; i++) marks[i] = newMarks[i];
    }
    // Display Student
    void displayStudent() {
        cout << "\nRoll Number: " << roll_number;
        cout << "\nName: " << name;
        cout << "\nMarks: ";
        for(int i = 0; i < 3; i++) {
            cout << marks[i] << " ";
        }
        cout << "\nAverage: " << calculateAverage() << endl;
    }
    // Calculate Average
    float calculateAverage() {
        float sum = 0;
        for(int i = 0; i < 3; i++) sum += marks[i];
        return sum / 3;
    }
    // Getter for roll number (for searching)
    int getRoll() {
        return roll_number;
    }
};
int main() {
    vector<Student> students;
    int choice;
    do {
        cout << "\n--- Student Record System ---\n";
        cout << "1. Add Student\n2. Modify Student\n3. Display All\n4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        if(choice == 1) {
            int r;
            string n;
            float m[3];
            cout << "Enter Roll Number: ";
            cin >> r;
            cout << "Enter Name: ";
            cin >> n;
            cout << "Enter 3 Marks: ";
            for(int i = 0; i < 3; i++) cin >> m[i];
            Student s(r, n, m);
            students.push_back(s);
        }
        else if(choice == 2) {
            int r;
            cout << "Enter Roll Number to modify: ";
            cin >> r;
            for(int i = 0; i < students.size(); i++) {
                if(students[i].getRoll() == r) {
                    string n;
                    float m[3];
                    cout << "Enter New Name: ";
                    cin >> n;
                    cout << "Enter New Marks: ";
                    for(int j = 0; j < 3; j++) cin >> m[j];

                    students[i].modifyStudent(n, m);
                }
            }
        }
        else if(choice == 3) {
            for(int i = 0; i < students.size(); i++) {
                students[i].displayStudent();
            }
        }
    } while(choice != 4);

    return 0;
}
```

# Employee Salary Management System Using File Handling

Scenario: You need to build an employee salary management system that reads employee records from a file, calculates their salary, and writes the updated data back to the file.

```cpp
#include <iostream>
#include <fstream>
#include <vector>
using namespace std;

class Employee {
private:
    int employee_id;
    string name;
    float salary;
public:
    Employee() {
        employee_id = 0;
        name = "Unknown";
        salary = 0;
    }
    Employee(int id, string n, float s) {
        employee_id = id;
        name = n;
        salary = s;
    }
    void calculateSalary() {
        float bonus = 0.10 * salary;      // 10% bonus
        float deduction = 0.05 * salary;  // 5% deduction
        salary = salary + bonus - deduction;
    }
    void display() {
        cout << "ID: " << employee_id 
             << ", Name: " << name 
             << ", Salary: " << salary << endl;
    }
    int getID() { return employee_id; }
    string getName() { return name; }
    float getSalary() { return salary; }
    void setSalary(float s) { salary = s; }
};
int main() {
    vector<Employee> employees;
    ifstream infile("employees.txt");
    // Exception Handling (File Check)
    if (!infile) {
        cout << "Error: File not found or cannot be opened!\n";
        return 1;
    }
    int id;
    string name;
    float salary;
    while (infile >> id >> name >> salary) {
        Employee emp(id, name, salary);
        employees.push_back(emp);
    }
    infile.close();
    // Processing salaries
    for (int i = 0; i < employees.size(); i++) {
        employees[i].calculateSalary();
    }
    // Writing updated data to file
    ofstream outfile("employees_updated.txt");
    if (!outfile) {
        cout << "Error: Cannot write to file!\n";
        return 1;
    }
    for (int i = 0; i < employees.size(); i++) {
        outfile << employees[i].getID() << " "
                << employees[i].getName() << " "
                << employees[i].getSalary() << endl;
    }
    outfile.close();
    // Display updated records
    cout << "\nUpdated Employee Records:\n";
    for (int i = 0; i < employees.size(); i++) {
        employees[i].display();
    }
    return 0;
}
```


#  Tic-Tac-Toe Game with Classes and Object-Oriented Design

Scenario: Develop a Tic-Tac-Toe game using object-oriented design principles. The game should allow two players to take turns, check for a winner, and reset the game.

```cpp
#include <iostream>
using namespace std;

class Game {
private:
    char board[3][3];
    char turn;     
    char winner;
public:
    Game() {
        resetGame();
    }
    void resetGame() {
        for(int i = 0; i < 3; i++)
            for(int j = 0; j < 3; j++)
                board[i][j] = ' ';
        turn = 'X';
        winner = ' ';
    }
    void printBoard() {
        cout << "\n";
        for(int i = 0; i < 3; i++) {
            cout << " ";
            for(int j = 0; j < 3; j++) {
                cout << board[i][j];
                if(j < 2) cout << " | ";
            }
            cout << "\n";
            if(i < 2) cout << "---|---|---\n";
        }
        cout << "\n";
    }
    bool makeMove(int row, int col) {
        if(row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            cout << "Invalid move! Try again.\n";
            return false;
        }
        board[row][col] = turn;
        turn = (turn == 'X') ? 'O' : 'X';
        return true;
    }
    void checkWinner() {
        // Rows & Columns
        for(int i = 0; i < 3; i++) {
            if(board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ')
                winner = board[i][0];

            if(board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
                winner = board[0][i];
        }
        if(board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
            winner = board[0][0];

        if(board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
            winner = board[0][2];
    }
    bool isDraw() {
        for(int i = 0; i < 3; i++)
            for(int j = 0; j < 3; j++)
                if(board[i][j] == ' ')
                    return false;
        return (winner == ' ');
    }
    char getWinner() {
        return winner;
    }
    char getTurn() {
        return turn;
    }
};
int main() {
    Game game;
    int row, col;
    cout << "=== Tic-Tac-Toe Game ===\n";
    while(true) {
        game.printBoard();
        cout << "Player " << game.getTurn() << ", enter row and column (0-2): ";
        cin >> row >> col;
        if(!game.makeMove(row, col))
            continue;
        game.checkWinner();
        if(game.getWinner() != ' ') {
            game.printBoard();
            cout << "Player " << game.getWinner() << " wins!\n";
            break;
        }
        if(game.isDraw()) {
            game.printBoard();
            cout << "It's a draw!\n";
            break;
        }
    }
    return 0;
}
'''
