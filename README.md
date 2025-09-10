#include <iostream>
#include <string>
#include <ctime>   // For University Cafe day menu
using namespace std;

// ===== Function Declarations =====
void teacherPortal();
void cafePortal();
void mainMenu();

// ===== Main Function =====
int main() {
    mainMenu();
    return 0;
}

// ===== Main Menu =====
void mainMenu() {
    int choice;
    do {
        cout << "\n===== University Management System =====" << endl;
        cout << "Press 1 for Teacher Portal" << endl;
        cout << "Press 2 for University Cafe" << endl;
        cout << "Press 0 to Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: teacherPortal(); break;
            case 2: cafePortal(); break;
            case 0: cout << "Exiting program... Goodbye!" << endl; break;
            default: cout << "Invalid choice. Try again." << endl;
        }
    } while(choice != 0);
}

// ===== Teacher Portal =====
void teacherPortal() {
    cout << "\n--- Teacher Portal ---" << endl;

    const int MAX_STUDENTS = 5;
    string studentNames[MAX_STUDENTS];
    int rollNumbers[MAX_STUDENTS];
    float labPerformance[MAX_STUDENTS];
    float labReports[MAX_STUDENTS];
    float midterm[MAX_STUDENTS];
    float cea[MAX_STUDENTS];
    float finalTerm[MAX_STUDENTS];
    float totalMarks[MAX_STUDENTS];
    char grade[MAX_STUDENTS];

    int numStudents;
    cout << "Enter number of students (max 5): ";
    cin >> numStudents;

    if (numStudents > MAX_STUDENTS) {
        cout << "Limit is 5 students. Setting to 5." << endl;
        numStudents = MAX_STUDENTS;
    }

    // --- Enter student data ---
    for (int i = 0; i < numStudents; i++) {
        cout << "\nEnter details for Student " << i + 1 << endl;
        cout << "Name: ";
        cin >> studentNames[i];
        cout << "Roll Number: ";
        cin >> rollNumbers[i];
        cout << "Marks in Lab Performance (out of 100): ";
        cin >> labPerformance[i];
        cout << "Marks in Lab Reports (out of 100): ";
        cin >> labReports[i];
        cout << "Marks in Midterm (out of 100): ";
        cin >> midterm[i];
        cout << "Marks in CEA (out of 100): ";
        cin >> cea[i];
        cout << "Marks in Final Term (out of 100): ";
        cin >> finalTerm[i];
    }

    // --- Assign weights ---
    float wLabPerf, wLabReports, wMid, wCea, wFinal;
    cout << "\nEnter weights for each assessment (total should = 100)" << endl;
    cout << "Lab Performance: "; cin >> wLabPerf;
    cout << "Lab Reports: "; cin >> wLabReports;
    cout << "Midterm: "; cin >> wMid;
    cout << "CEA: "; cin >> wCea;
    cout << "Final Term: "; cin >> wFinal;

    // --- Calculate total marks and grades ---
    for (int i = 0; i < numStudents; i++) {
        totalMarks[i] = (labPerformance[i] * wLabPerf / 100) +
                        (labReports[i] * wLabReports / 100) +
                        (midterm[i] * wMid / 100) +
                        (cea[i] * wCea / 100) +
                        (finalTerm[i] * wFinal / 100);

        if (totalMarks[i] >= 85) grade[i] = 'A';
        else if (totalMarks[i] >= 70) grade[i] = 'B';
        else if (totalMarks[i] >= 55) grade[i] = 'C';
        else if (totalMarks[i] >= 40) grade[i] = 'D';
        else grade[i] = 'F';
    }

    // --- Display Results ---
    cout << "\n===== Final Results =====" << endl;
    for (int i = 0; i < numStudents; i++) {
        cout << "Student: " << studentNames[i]
             << " | Roll: " << rollNumbers[i]
             << " | Total: " << totalMarks[i]
             << " | Grade: " << grade[i] << endl;
    }
}

// ===== University Cafe =====
void cafePortal() {
    cout << "\n--- University Cafe ---" << endl;

    time_t t = time(0);
    tm* now = localtime(&t);
    int day = now->tm_wday;

    string menu[7][10] = {
        {"Burger", "Fries", "Pizza", "Pasta", "Sandwich", "Donut", "Coffee", "Tea", "Ice Cream", "Juice"},
        {"Chicken Biryani", "Kebab", "Roti", "Salad", "Soup", "Cake", "Juice", "Lassi", "Tea", "Coffee"},
        {"Beef Biryani", "Burger", "Wrap", "Shawarma", "Fries", "Muffin", "Tea", "Coffee", "Ice Cream", "Juice"},
        {"Chicken Karahi", "Naan", "Salad", "Soup", "Pizza", "Cake", "Tea", "Coffee", "Juice", "Milkshake"},
        {"Pulao", "BBQ", "Burger", "Shawarma", "Roll", "Donut", "Tea", "Coffee", "Ice Cream", "Juice"},
        {"Mutton Biryani", "Seekh Kebab", "Paratha", "Omelette", "Fries", "Cake", "Tea", "Coffee", "Juice", "Milkshake"},
        {"Chicken Handi", "Roti", "Salad", "Soup", "Burger", "Wrap", "Tea", "Coffee", "Cake", "Juice"}
    };

    int prices[7][10] = {
        {250, 100, 500, 400, 200, 120, 100, 80, 150, 120},
        {300, 200, 200, 100, 150, 200, 120, 150, 80, 100},
        {350, 250, 200, 220, 100, 180, 80, 100, 150, 120},
        {400, 200, 100, 150, 500, 220, 80, 100, 120, 200},
        {280, 300, 250, 200, 180, 120, 80, 100, 150, 120},
        {500, 250, 150, 100, 120, 200, 80, 100, 120, 150},
        {450, 200, 100, 150, 250, 200, 80, 100, 200, 150}
    };

    cout << "\nToday's Menu:" << endl;
    for (int i = 0; i < 10; i++) {
        cout << i+1 << ". " << menu[day][i] << " - Rs." << prices[day][i] << endl;
    }

    int choice, totalBill = 0;
    string more;

    do {
        cout << "\nEnter item number to buy (1-10): ";
        cin >> choice;
        if (choice >= 1 && choice <= 10) {
            totalBill += prices[day][choice-1];
            cout << menu[day][choice-1] << " added to your bill." << endl;
        } else {
            cout << "Invalid choice!" << endl;
        }
        cout << "Do you want to buy more items? (yes/no): ";
        cin >> more;
    } while (more == "yes");

    cout << "\nYour total bill is: Rs." << totalBill << endl;
}
