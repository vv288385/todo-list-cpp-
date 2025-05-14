

Overview:

A simple command-line To-Do List Manager written in C++. This project allows users to add, view, mark as done, and delete tasks.


---

Features:

Add new tasks

View all tasks

Mark tasks as completed

Delete tasks

Save tasks to a file

Load tasks from a file



---

Technologies Used:

C++

File Handling



---

Sample Code Structure:

#include <iostream>
#include <fstream>
#include <vector>
using namespace std;

struct Task {
    string description;
    bool isDone;
};

vector<Task> tasks;

void addTask() {
    Task t;
    cout << "Enter task description: ";
    cin.ignore();
    getline(cin, t.description);
    t.isDone = false;
    tasks.push_back(t);
    cout << "Task added.\n";
}

void showTasks() {
    for (int i = 0; i < tasks.size(); ++i) {
        cout << i+1 << ". " << tasks[i].description 
             << (tasks[i].isDone ? " [Done]" : "") << endl;
    }
}

void markDone() {
    int index;
    cout << "Enter task number to mark as done: ";
    cin >> index;
    if (index > 0 && index <= tasks.size()) {
        tasks[index-1].isDone = true;
        cout << "Task marked as done.\n";
    } else {
        cout << "Invalid index.\n";
    }
}

void deleteTask() {
    int index;
    cout << "Enter task number to delete: ";
    cin >> index;
    if (index > 0 && index <= tasks.size()) {
        tasks.erase(tasks.begin() + index - 1);
        cout << "Task deleted.\n";
    } else {
        cout << "Invalid index.\n";
    }
}

void saveTasks() {
    ofstream file("tasks.txt");
    for (const auto& t : tasks) {
        file << t.description << "|" << t.isDone << endl;
    }
    file.close();
    cout << "Tasks saved.\n";
}

void loadTasks() {
    tasks.clear();
    ifstream file("tasks.txt");
    string desc;
    bool done;
    while (getline(file, desc, '|') && file >> done) {
        file.ignore();
        tasks.push_back({desc, done});
    }
    file.close();
}

int main() {
    loadTasks();
    int choice;
    do {
        cout << "\n1. Add Task\n2. Show Tasks\n3. Mark as Done\n4. Delete Task\n5. Save and Exit\nChoose: ";
        cin >> choice;
        switch (choice) {
            case 1: addTask(); break;
            case 2: showTasks(); break;
            case 3: markDone(); break;
            case 4: deleteTask(); break;
            case 5: saveTasks(); break;
        }
    } while (choice != 5);
    return 0;
}




