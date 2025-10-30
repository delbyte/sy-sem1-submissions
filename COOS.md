# Computer Organization and Operating Systems Assignments Accompanying Notes

## Assignment 1: Study of Operating Systems

**Aim:** To study and understand the different types of operating systems, their characteristics, and their applications.

**Theory:**
An Operating System (OS) is system software that manages computer hardware and software resources and provides common services for computer programs. The OS is a component of the system software in a computer system. Application programs usually require an operating system to function.

**Types of Operating Systems:**
*   **Batch Operating System:** In a batch OS, jobs with similar needs are batched together and executed as a group. The users of a batch operating system do not interact with the computer directly. Each user prepares his job on an off-line device like punch cards and submits it to the computer operator.
*   **Time-Sharing Operating System:** Time-sharing is a technique which enables many people, located at various terminals, to use a particular computer system at the same time. Time-sharing or multitasking is a logical extension of multiprogramming. The processor's time which is shared among multiple users simultaneously is termed as time-sharing.
*   **Distributed Operating System:** A distributed operating system is a software over a collection of independent, networked, communicating, and physically separate computational nodes. They handle jobs which are serviced by multiple CPUs. Each individual node holds a specific software subset of the global aggregate operating system.
*   **Network Operating System:** A network operating system (NOS) is a computer operating system that is designed primarily to support workstations, personal computers and, in some instances, older terminals that are connected on a local area network (LAN).
*   **Real-Time Operating System (RTOS):** A real-time operating system (RTOS) is an operating system (OS) intended to serve real-time applications that process data as it comes in, typically without buffer delays. Processing time requirements are measured in tenths of seconds or shorter.

**Applications:**
*   **Batch OS:** Payroll systems, bank statements, scientific calculations.
*   **Time-Sharing OS:** Mainframes, minicomputers, and modern desktop operating systems.
*   **Distributed OS:** Cloud computing, high-performance computing clusters.
*   **Network OS:** File servers, print servers, and other network services.
*   **RTOS:** Industrial control systems, robotics, avionics, and medical devices.

**Conclusion:**
Each type of operating system is designed for a specific purpose and has its own set of advantages and disadvantages. The choice of an operating system depends on the requirements of the application.

## Assignment 2: Simple Calculator in Assembly Language

**Aim:** To implement a simple calculator for arithmetic operations using Assembly Language.

**Theory:**
Assembly language is a low-level programming language that has a very strong correspondence between the instructions in the language and the architecture's machine code instructions. It is specific to a particular computer architecture. Writing a calculator in assembly involves direct manipulation of CPU registers (like EAX, EBX, etc. in x86) to store numbers and using specific instructions (like `ADD`, `SUB`, `MUL`, `DIV`) to perform arithmetic. It also requires understanding how to interact with the operating system for input/output, which is done via system calls.

**Applications:**
*   Performance-critical parts of applications.
*   Device drivers and other hardware-interacting programs.
*   Embedded systems and firmware.
*   Reverse engineering and debugging.

**Example Code (x86 Assembly - NASM):**
```assembly
section .data
    msg db "Result is: "
    len equ $ - msg

section .bss
    result resb 1

section .text
    global _start

_start:
    mov eax, 5
    mov ebx, 3
    add eax, ebx  ; 5 + 3 = 8

    ; (code to convert eax to ASCII and print would go here)

    mov eax, 1
    int 0x80
```

**Conclusion:**
Implementing a simple calculator in assembly language provides a fundamental understanding of how arithmetic operations are performed at the hardware level and how to interact with the processor's registers and the operating system.

## Assignment 3: Booth's Algorithm

**Aim:** To implement Booth's algorithm for binary multiplication.

**Theory:**
Booth's algorithm is a multiplication algorithm that multiplies two signed binary numbers in two's complement notation. The algorithm is efficient because it can handle both positive and negative numbers and it can skip over blocks of identical bits. It works by repeatedly adding or subtracting the multiplicand to or from the partial product, based on the current and previous bits of the multiplier.

**Applications:**
*   Used in the design of computer arithmetic logic units (ALUs).
*   Efficient for multiplying signed numbers in hardware.

**Example Code (C++):**
```cpp
#include <iostream>

void boothAlgorithm(int br, int qr) {
    int ac = 0, n = 5;
    int mt = br;
    int sc = n;
    while (sc > 0) {
        if ((qr & 1) == 1) {
            ac = ac + mt;
        }
        qr = qr >> 1;
        mt = mt << 1;
        sc--;
    }
    std::cout << "Result: " << ac << std::endl;
}

int main() {
    boothAlgorithm(5, 3);
    return 0;
}
```

**Conclusion:**
Booth's algorithm is an efficient method for signed binary multiplication that is widely used in computer hardware. Understanding this algorithm is essential for computer organization and architecture.

## Assignment 4: Restoring and Non-Restoring Division

**Aim:** To implement the Restoring and Non-Restoring division algorithms for binary numbers.

**Theory:**
*   **Restoring Division:** This is a simple but slow division algorithm. In each step, it shifts the dividend and subtracts the divisor. If the result is negative, the divisor is added back (restoring the previous value), and a 0 is placed in the quotient. Otherwise, a 1 is placed in the quotient.
*   **Non-Restoring Division:** This is a more efficient division algorithm that avoids the restoring step. It involves a cycle of shifting and either adding or subtracting the divisor based on the sign of the partial remainder. This reduces the number of operations compared to the restoring method.

**Applications:**
*   Used in the implementation of division in computer ALUs.

**Example Code (C++ for Restoring Division):**
```cpp
#include <iostream>

void restoringDivision(int dividend, int divisor) {
    int accumulator = 0;
    int n = 4; // Number of bits
    for (int i = 0; i < n; i++) {
        accumulator = (accumulator << 1) | ((dividend >> (n - 1 - i)) & 1);
        accumulator = accumulator - divisor;
        if (accumulator < 0) {
            std::cout << "0";
            accumulator = accumulator + divisor;
        } else {
            std::cout << "1";
        }
    }
    std::cout << std::endl;
}

int main() {
    restoringDivision(8, 3);
    return 0;
}
```

**Conclusion:**
Restoring and Non-Restoring division are two fundamental algorithms for binary division. Non-Restoring division is generally faster as it avoids the time-consuming restoring step, making it more suitable for hardware implementation.

## Assignment 5: CPU Scheduling Algorithms

**Aim:** To implement the SJF (Shortest Job First) and FCFS (First Come First Served) CPU scheduling algorithms.

**Theory:**
CPU scheduling is the process of determining which process will own the CPU for execution while another process is on hold. 
*   **FCFS (First Come First Served):** This is the simplest CPU scheduling algorithm. The process that requests the CPU first is allocated the CPU first. It is a non-preemptive algorithm.
*   **SJF (Shortest Job First):** This algorithm associates with each process the length of its next CPU burst. When the CPU is available, it is assigned to the process that has the smallest next CPU burst. This can be either preemptive or non-preemptive.

**Applications:**
*   Used in operating systems to determine which process should be executed by the CPU to optimize system performance (e.g., minimize waiting time, maximize throughput).

**Example Code (C++ for FCFS):**
```cpp
#include <iostream>
#include <vector>

void findWaitingTime(const std::vector<int>& bt, std::vector<int>& wt) {
    wt[0] = 0;
    for (int i = 1; i < bt.size(); i++) {
        wt[i] = bt[i - 1] + wt[i - 1];
    }
}

int main() {
    std::vector<int> burst_time = {10, 5, 8};
    std::vector<int> waiting_time(burst_time.size());
    findWaitingTime(burst_time, waiting_time);
    std::cout << "Process " << 1 << " waiting time: " << waiting_time[0] << std::endl;
    std::cout << "Process " << 2 << " waiting time: " << waiting_time[1] << std::endl;
    std::cout << "Process " << 3 << " waiting time: " << waiting_time[2] << std::endl;
    return 0;
}
```

**Conclusion:**
FCFS is simple to implement but can lead to long waiting times (convoy effect). SJF is optimal in terms of average waiting time, but it is difficult to predict the length of the next CPU burst, making its practical implementation challenging.

## Assignment 6: Banker's Algorithm

**Aim:** To implement the Banker's Algorithm for deadlock avoidance.

**Theory:**
The Banker's Algorithm is a resource allocation and deadlock avoidance algorithm developed by Edsger Dijkstra. It tests for safety by simulating the allocation for predetermined maximum possible amounts of all resources, then makes a "safe-state" check to test for possible deadlocks for all other pending activities, before deciding whether allocation should be allowed to continue. For the Banker's algorithm to work, it needs to know the maximum number of each resource that a process can request.

**Applications:**
*   Used in operating systems to avoid deadlock and ensure that the system remains in a safe state.

**Example Code (C++):**
```cpp
#include <iostream>
#include <vector>

int main() {
    int n = 5; // Number of processes
    int m = 3; // Number of resources
    std::vector<std::vector<int>> allocation = {{0, 1, 0}, {2, 0, 0}, {3, 0, 2}, {2, 1, 1}, {0, 0, 2}};
    std::vector<std::vector<int>> max = {{7, 5, 3}, {3, 2, 2}, {9, 0, 2}, {2, 2, 2}, {4, 3, 3}};
    std::vector<int> available = {3, 3, 2};

    // (Banker's algorithm logic would go here)

    std::cout << "Banker\'s algorithm logic is complex to demonstrate in a short snippet." << std::endl;

    return 0;
}
```

**Conclusion:**
The Banker's Algorithm is a classic and important algorithm for deadlock avoidance. While it has some overhead and requires prior knowledge of maximum resource needs, it provides a robust way to prevent deadlocks in a system.

## Assignment 7: Page Replacement Algorithms

**Aim:** To implement the Optimal and LRU (Least Recently Used) page replacement algorithms.

**Theory:**
In a virtual memory system, page replacement algorithms decide which memory pages to page out (swap out, write to disk) when a page of memory needs to be allocated. 
*   **Optimal Page Replacement:** This algorithm has the lowest page fault rate of all algorithms. It replaces the page that will not be used for the longest period of time. It is impossible to implement in a real system because it requires future knowledge.
*   **LRU (Least Recently Used):** This algorithm replaces the page that has not been used for the longest period of time. It is a good approximation of the optimal algorithm and is widely used in practice. It can be implemented using a counter or a stack.

**Applications:**
*   Used in the memory management unit of operating systems to manage virtual memory and handle page faults.

**Example Code (C++ for LRU):**
```cpp
#include <iostream>
#include <vector>
#include <list>
#include <unordered_map>

class LRUCache {
    int capacity;
    std::list<int> dq;
    std::unordered_map<int, std::list<int>::iterator> ma;

public:
    LRUCache(int n) {
        capacity = n;
    }

    void refer(int x) {
        if (ma.find(x) == ma.end()) {
            if (dq.size() == capacity) {
                int last = dq.back();
                dq.pop_back();
                ma.erase(last);
            }
        } else {
            dq.erase(ma[x]);
        }
        dq.push_front(x);
        ma[x] = dq.begin();
    }

    void display() {
        for (auto it = dq.begin(); it != dq.end(); it++)
            std::cout << (*it) << " ";
        std::cout << std::endl;
    }
};

int main() {
    LRUCache ca(4);
    ca.refer(1);
    ca.refer(2);
    ca.refer(3);
    ca.refer(1);
    ca.refer(4);
    ca.refer(5);
    ca.display();
    return 0;
}
```

**Conclusion:**
Optimal page replacement is the theoretical benchmark for page replacement algorithms. LRU is a practical and widely used algorithm that provides good performance by approximating the optimal algorithm.

## Assignment 8: Simple Text Editor

**Aim:** To implement a simple text editor.

**Theory:**
A simple text editor can be implemented using basic data structures to store the lines of text. A common approach is to use a dynamic array (like `std::vector` in C++) or a linked list of strings, where each string represents a line. The program should be able to read a file into this buffer, allow for basic editing operations (like inserting and deleting lines), and write the buffer back to a file.

**Applications:**
*   This is a fundamental application that demonstrates file I/O and data structure manipulation.
*   It serves as a basis for understanding more complex text editors and word processors.

**Example Code (C++):**
```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>

int main() {
    std::vector<std::string> buffer;
    std::string line;
    std::ifstream file("test.txt");
    if (file.is_open()) {
        while (getline(file, line)) {
            buffer.push_back(line);
        }
        file.close();
    }

    // (code for editing and saving the buffer would go here)
    // For example, to add a line:
    buffer.push_back("A new line.");

    std::ofstream outFile("test.txt");
    for (const auto &l : buffer) {
        outFile << l << std::endl;
    }
    outFile.close();

    return 0;
}
```

**Conclusion:**
Implementing a simple text editor is a great way to learn about file handling, string manipulation, and the use of data structures to manage a text buffer. It is a practical exercise that combines several fundamental programming concepts.

## Assignment 9: Simple File Management System

**Aim:** To implement a simple file management system.

**Theory:**
A file management system can be simulated using a hierarchical data structure like a tree to represent the directory structure. Each node in the tree can represent either a file or a directory. A directory node would contain a list of its children (files and subdirectories). The system should support basic commands like `mkdir` (make directory), `cd` (change directory), `ls` (list contents), and `touch` (create a file).

**Applications:**
*   This project helps in understanding the basic principles of how operating systems manage files and directories.
*   It provides a practical understanding of tree data structures.

**Example Code (C++):**
```cpp
#include <iostream>
#include <map>
#include <string>

struct Node {
    std::map<std::string, Node*> children;
    bool isDir;
};

// (A full implementation is lengthy)

int main() {
    std::cout << "File system simulation is a good exercise in tree data structures." << std::endl;
    return 0;
}
```

**Conclusion:**
Implementing a file management system provides insight into the data structures and algorithms used by operating systems to organize and provide access to files in a hierarchical manner.

## Assignment 10: Linux Commands

**Aim:** To study and practice various Linux commands.

**Theory:**
Linux is a family of open-source Unix-like operating systems based on the Linux kernel. The command line is a powerful tool for interacting with a Linux system. It allows users to perform a wide range of tasks, from simple file manipulation to complex system administration.

**Common Commands:**

*   **File Management:**
    *   `ls`: List directory contents.
    *   `cd`: Change directory.
    *   `pwd`: Print working directory.
    *   `cp`: Copy files and directories.
    *   `mv`: Move or rename files and directories.
    *   `rm`: Remove files and directories.
    *   `mkdir`: Create a new directory.
    *   `touch`: Create an empty file.

*   **Text Processing:**
    *   `cat`: Concatenate and display files.
    *   `grep`: Search for patterns in files.
    *   `sed`: Stream editor for filtering and transforming text.
    *   `awk`: A powerful pattern scanning and processing language.
    *   `head`: Output the first part of files.
    *   `tail`: Output the last part of files.

*   **Process Management:**
    *   `ps`: Report a snapshot of the current processes.
    *   `top`: Display Linux processes.
    *   `kill`: Send a signal to a process.
    *   `bg`: Put a job in the background.
    *   `fg`: Bring a job to the foreground.

*   **System Information:**
    *   `uname`: Print system information.
    *   `df`: Report file system disk space usage.
    *   `free`: Display amount of free and used memory in the system.

**Conclusion:**
Mastering the Linux command line is a fundamental skill for anyone working with Linux systems. It provides a powerful and flexible way to manage and interact with the operating system.

## Assignment 11: Shell Scripting

**Aim:** To learn the basics of shell scripting.

**Theory:**
A shell script is a computer program designed to be run by the Unix/Linux shell, a command-line interpreter. It is a text file containing a sequence of commands for a shell to execute. Shell scripts can be used to automate repetitive tasks, perform complex operations by combining simple commands, and create new custom commands. Common shells include Bash, Zsh, and Fish.

**Applications:**
*   Automating system administration tasks (e.g., backups, user management).
*   Creating custom commands and tools.
*   Simplifying complex workflows and deployment processes.

**Example Code (Bash):**
```bash
#!/bin/bash

# A simple script to greet the user

echo "Enter your name:"
read name
echo "Hello, $name!"
```

**Conclusion:**
Shell scripting is a powerful tool for automation and customization in a Linux/Unix environment. It is a valuable skill for anyone working with these operating systems, from developers to system administrators.
