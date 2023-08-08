#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>

struct Student {
    std::string stream;
    std::string className;
    int studentID;
    double subject1Marks;
    double subject2Marks;
    double subject3Marks;
    double totalMarks;
    int schoolRank;
    int classRank;
};

bool compareStudents(const Student &a, const Student &b) {
    return a.totalMarks > b.totalMarks;
}

void calculateRanks(std::vector<Student> &students) {
    std::sort(students.begin(), students.end(), compareStudents);

    int currentRank = 1;
    for (size_t i = 0; i < students.size(); ++i) {
        students[i].schoolRank = currentRank;

        if (i > 0 && students[i].totalMarks < students[i - 1].totalMarks) {
            currentRank = i + 1;
        }
    }

    for (size_t i = 0; i < students.size(); ++i) {
        int classRank = 1;
        for (size_t j = 0; j < students.size(); ++j) {
            if (students[j].stream == students[i].stream && students[j].className == students[i].className &&
                students[j].totalMarks > students[i].totalMarks) {
                classRank++;
            }
        }
        students[i].classRank = classRank;
    }
}

int main() {
    std::ifstream inputFile("student_marks.txt");
    if (!inputFile) {
        std::cerr << "Error opening file!" << std::endl;
        return 1;
    }

    std::vector<Student> students;
    std::string stream, className;
    int studentID;
    double subject1, subject2, subject3;

    while (inputFile >> stream >> className >> studentID >> subject1 >> subject2 >> subject3) {
        Student student;
        student.stream = stream;
        student.className = className;
        student.studentID = studentID;
        student.subject1Marks = subject1;
        student.subject2Marks = subject2;
        student.subject3Marks = subject3;
        student.totalMarks = subject1 + subject2 + subject3;
        students.push_back(student);
    }

    inputFile.close();

    calculateRanks(students);

    // Print and write ranks to file
    std::ofstream outputFile("rank_results.txt");
    if (!outputFile) {
        std::cerr << "Error opening file for writing!" << std::endl;
        return 1;
    }

    for (const Student &student : students) {
        std::cout << "Student ID: " << student.studentID << "\n"
                  << "Stream: " << student.stream << "\n"
                  << "Class: " << student.className << "\n"
                  << "Total Marks: " << student.totalMarks << "\n"
                  << "School Rank: " << student.schoolRank << "\n"
                  << "Class Rank: " << student.classRank << "\n\n";

        outputFile << "Student ID: " << student.studentID << "\n"
                   << "Stream: " << student.stream << "\n"
                   << "Class: " << student.className << "\n"
                   << "Total Marks: " << student.totalMarks << "\n"
                   << "School Rank: " << student.schoolRank << "\n"
                   << "Class Rank: " << student.classRank << "\n\n";
    }

    outputFile.close();

    return 0;
}
