# week-3
The n-queens is the problem of placing n queens on n × n chessboard such
that no two queens can attack each other. Given an integer n, return all
distinct solutions to the n -queens puzzle. Each solution contains a distinct
boards configuration of the queen's placement, where ‘Q’ and ‘.’ indicate
queen and empty space respectively.

#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> result;
        vector<string> board(n, string(n, '.'));
        vector<int> leftRow(n, 0), upperDiagonal(2 * n - 1, 0), lowerDiagonal(2 * n - 1, 0);
        solve(0, board, result, leftRow, upperDiagonal, lowerDiagonal, n);
        return result;
    }

private:
    void solve(int col, vector<string>& board, vector<vector<string>>& result,
               vector<int>& leftRow, vector<int>& upperDiagonal, vector<int>& lowerDiagonal, int n) {
        if (col == n) {
            result.push_back(board);
            return;
        }

        for (int row = 0; row < n; row++) {
            if (leftRow[row] == 0 && lowerDiagonal[row + col] == 0 && upperDiagonal[n - 1 + col - row] == 0) {
                board[row][col] = 'Q';
                leftRow[row] = 1;
                lowerDiagonal[row + col] = 1;
                upperDiagonal[n - 1 + col - row] = 1;

                solve(col + 1, board, result, leftRow, upperDiagonal, lowerDiagonal, n);

                board[row][col] = '.';
                leftRow[row] = 0;
                lowerDiagonal[row + col] = 0;
                upperDiagonal[n - 1 + col - row] = 0;
            }
        }
    }
};

int main() {
    int n;
    cout << "Enter the value of n: ";
    cin >> n;

    Solution solution;
    vector<vector<string>> solutions = solution.solveNQueens(n);

    cout << "Number of solutions: " << solutions.size() << endl;
    for (const auto& solution : solutions) {
        for (const auto& row : solution) {
            cout << row << endl;
        }
        cout << endl;
    }

    return 0;
}



Find the smallest element in a list.

#include <iostream>
#include <vector>
#include <limits.h> 

using namespace std;

int findSmallestElement(const vector<int>& arr) {
    int smallest = INT_MAX; 

    for (int num : arr) {
        if (num < smallest) {
            smallest = num;
        }
    }

    return smallest;
}

int main() {
    int n;
    cout << "Enter the number of elements: ";
    cin >> n;

    vector<int> arr(n);
    cout << "Enter the elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    int smallest = findSmallestElement(arr);
    cout << "The smallest element is: " << smallest << endl;

    return 0;
}


Write a program that converts units (e.g., length, weight, temperature)
between different measurement systems.

#include <iostream>
using namespace std;

void convertLength() {
    double value;
    cout << "Enter value in meters: ";
    cin >> value;

    cout << "In kilometers: " << value / 1000 << " km" << endl;
    cout << "In centimeters: " << value * 100 << " cm" << endl;
    cout << "In inches: " << value * 39.3701 << " in" << endl;
    cout << "In feet: " << value * 3.28084 << " ft" << endl;
}

void convertWeight() {
    double value;
    cout << "Enter value in kilograms: ";
    cin >> value;

    cout << "In grams: " << value * 1000 << " g" << endl;
    cout << "In pounds: " << value * 2.20462 << " lbs" << endl;
    cout << "In ounces: " << value * 35.274 << " oz" << endl;
}

void convertTemperature() {
    double value;
    cout << "Enter value in Celsius: ";
    cin >> value;

    double fahrenheit = (value * 9/5) + 32;
    double kelvin = value + 273.15;

    cout << "In Fahrenheit: " << fahrenheit << " °F" << endl;
    cout << "In Kelvin: " << kelvin << " K" << endl;
}

int main() {
    int choice;

    while (true) {
        cout << "Unit Conversion Menu:\n";
        cout << "1. Convert Length (Meters)\n";
        cout << "2. Convert Weight (Kilograms)\n";
        cout << "3. Convert Temperature (Celsius)\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                convertLength();
                break;
            case 2:
                convertWeight();
                break;
            case 3:
                convertTemperature();
                break;
            case 4:
                cout << "Exiting program..." << endl;
                return 0;
            default:
                cout << "Invalid choice, please try again." << endl;
        }

        cout << endl;
    }

    return 0;
}

Develop a system to manage a library's catalog, including adding
books, checking out books, and returning books

#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Book {
    string title;
    string author;
    bool isAvailable;
