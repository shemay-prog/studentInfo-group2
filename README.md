#include <iostream>
#include <string>

using namespace std;

struct StudentInfo {
    string firstN, lastN, section, course;
    int year = 0;
};

int MainMenu();
void StudentInformationInput(StudentInfo students[], int& numStudents, const int& MAXSTUDENTS);
void DisplayStudentInfo(StudentInfo students[], int& numStudents, const int& MAXSTUDENTS);

int main() {
    const int MAXSTUDENTS = 100;
    StudentInfo students[MAXSTUDENTS];
    int numStudents = 0;
    int choice;

    do {
        choice = MainMenu();

        switch (choice) {
        case 1:
            system("cls");
            StudentInformationInput(students, numStudents, MAXSTUDENTS);
            break;

        case 2:
            system("cls");
            DisplayStudentInfo(students, numStudents, MAXSTUDENTS);
            break;

        case 3:
            system("cls");
            cout << "Goodbye!\n";
            return 0;
        }
    } while (choice != 3);

    return 0;
}

int MainMenu() {
    int choice;

    cout << "\nStudent Information System\n";
    cout << "1. Add student\n";
    cout << "2. View student(s)\n";
    cout << "3. Exit\n\n";
    cout << "Enter your choice: ";
    cin >> choice;

    return choice;
}

void StudentInformationInput(StudentInfo students[], int& numStudents, const int& MAXSTUDENTS) {
    if (numStudents < MAXSTUDENTS) { // Check if there's space for a new student
        cout << "\nStudent Information Input\n";

        StudentInfo& stud = students[numStudents];

        cout << "First name: ";
        cin >> stud.firstN;

        cout << "Last name: ";
        cin >> stud.lastN;

        cout << "Year: ";
        cin >> stud.year;

        cout << "Section: ";
        cin >> stud.section;

        cout << "Course: ";
        cin >> stud.course;

        numStudents++;
    }
    else {
        cout << "Maximum number of students reached!\n";
    }
}

void DisplayStudentInfo(StudentInfo students[], int& numStudents, const int& MAXSTUDENTS)
{
    StudentInfo stud;
    const int STUDENTS_PER_PAGE = 5;
    int totalPages = (numStudents - 1) / STUDENTS_PER_PAGE + 1;
    int currentPage = 0;
    char option;

    if (numStudents)
    {
        cout << "Student Information Display\n\n";

        cout << "Page " << currentPage + 1 << " of " << totalPages << "\n\n";
        for (int i = currentPage * STUDENTS_PER_PAGE; i < min((currentPage + 1) * STUDENTS_PER_PAGE, numStudents); ++i)
        {
            stud = students[i];

            cout << "Student " << i + 1 << ":\n";
            cout << "First name: " << stud.firstN << endl;
            cout << "Last name: " << stud.lastN << endl;
            cout << "Year: " << stud.year << endl;
            cout << "Section: " << stud.section << endl;
            cout << "Course: " << stud.course << endl << endl;
        }

        if (numStudents >= 5) {
            cout << "N - Next Page, P - Previous Page, E - Exit to Main Menu\n";
            cout << "Enter option: ";
            cin >> option;

            switch (option)
            {
            case 'N':
            case 'n':
                if (currentPage < totalPages - 1)
                {
                    currentPage++;
                }
                else {
                    cout << "\nThere's no more next page\n";
                    DisplayStudentInfo(students, numStudents, MAXSTUDENTS);
                    break;
                }
                break;
            case 'P':
            case 'p':
                if (currentPage > 0)
                {
                    currentPage--;
                }
                break;
            } while (option != 'E' && option != 'e');
        }

        system("pause");
        system("cls");
    } 
    else 
    {
        cout << "There's no student information yet.\n\n";
    }
}
