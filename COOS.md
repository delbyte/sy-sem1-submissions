# Computer Organization and Operating Systems Assignments

This document contains short assignment descriptions with concise theory, applications, and compact, runnable example implementations where appropriate. The goal is to keep each assignment explanation practical and educational while providing a working snippet to try locally.

## Assignment 1: Study of Operating Systems

**Aim:** To study and understand the different types of operating systems, their characteristics, and their applications.

**Theory (expanded):**
An Operating System (OS) manages hardware resources and provides services to applications. It abstracts details of devices, schedules CPU and I/O, manages memory, and enforces protection and security. Key components include kernel, device drivers, file system, process and memory managers, and system call interface.

Different types of operating systems and when to pick them:
- **Batch OS:** Suitable when many similar jobs run offline (e.g., payroll). Minimal interactive overhead.
- **Time-Shared OS:** Good for interactive multi-user systems (terminals, academic clusters). Uses short time slices to maintain responsiveness.
- **Distributed OS:** Useful for cluster/cloud computing where transparency and fault-tolerance are required.
- **Network OS:** Focused on file and user management across a network — common in enterprise servers.
- **RTOS:** Required in embedded or control systems where deadlines are strict (automotive, avionics).

**Practical notes:**
- Performance vs. fairness: schedulers trade throughput for response. Embedded systems prefer predictability over throughput.
- Virtual memory allows processes to run with the illusion of more RAM; swapping policy impacts latency.

**Applications:**
- Batch: financial and batch-reporting systems.
- Time-sharing: university systems, shared HPC front-ends.
- Distributed: distributed databases, cloud platforms.
- RTOS: motor control, medical devices.

**Conclusion:**
Understanding OS types helps select the right abstractions and architecture for an application domain.

## Assignment 2: Simple Calculator in Assembly Language

**Aim:** Implement a small calculator in assembly to demonstrate low-level arithmetic and I/O.

**Theory (expanded):**
Assembly exposes registers, flags, and direct arithmetic instructions. Writing a calculator shows how addition, subtraction, multiplication (via repeated add or MUL), and division (DIV instruction) map to machine ops. You'll also learn integer to ASCII conversion and system I/O.

**Applications:**
- Bootloaders, tiny embedded routines, educational tools.

**Example Code (x86 NASM — Linux/x86 32-bit):**
This is a minimal program that computes 2 + 3 and prints the decimal result. It focuses on the calculation and conversion to ASCII; syscall conventions vary by platform.
```assembly
; calc.asm - nasm x86 (32-bit) example
; assemble: nasm -felf32 calc.asm && ld -m elf_i386 calc.o -o calc
section .data
    prefix db "Result: ", 0
section .bss
    buf resb 12
section .text
    global _start

_start:
    mov eax, 2
    add eax, 3        ; eax = 5

    ; convert eax (positive) to ASCII in buf
    mov ebx, 10
    mov ecx, buf
    add ecx, 11
    mov byte [ecx], 0
    dec ecx
    cmp eax, 0
    jne .conv
    mov byte [ecx], '0'
    dec ecx
    jmp .print
.conv:
    xor edx, edx
.loop:
    xor edx, edx
    div ebx
    add dl, '0'
    mov [ecx], dl
    dec ecx
    cmp eax, 0
    jne .loop
    inc ecx
.print:
    ; write prefix
    mov eax, 4
    mov ebx, 1
    mov ecx, prefix
    mov edx, 8
    int 0x80
    ; write number
    mov eax, 4
    mov ebx, 1
    mov edx, 11
    int 0x80
    ; exit
    mov eax, 1
    xor ebx, ebx
    int 0x80
```

**Notes:**
- This example is Linux/x86 specific; Windows uses different syscalls. To extend, read input and parse numbers or implement a simple REPL.

## Assignment 3: Booth's Algorithm

**Aim:** Implement Booth's algorithm for signed binary multiplication.

**Theory (expanded):**
Booth's algorithm reduces partial products by encoding runs of 1s in the multiplier. It examines pairs of bits (current LSB and a virtual previous bit) and decides whether to add, subtract, or do nothing, then performs an arithmetic shift.

**Applications:**
- Hardware multipliers in ALUs, DSPs.

**Compact C++ Example (demonstrative):**
The following demonstrates the Booth idea for 32-bit operands and is educational rather than highly optimized for production hardware.
```cpp
#include <iostream>
#include <cstdint>
using namespace std;

int64_t booth32(int32_t m, int32_t r) {
    int64_t A = 0;
    int64_t M = (int64_t)(int32_t)m;
    uint64_t Q = (uint32_t)r;
    int Q_1 = 0;
    for (int i = 0; i < 32; ++i) {
        int Q0 = Q & 1;
        if (Q0 == 1 && Q_1 == 0) A -= M;
        else if (Q0 == 0 && Q_1 == 1) A += M;
        // arithmetic right shift of [A,Q,Q_1]
        int64_t combined = (A << 32) | Q;
        combined >>= 1; // arithmetic shift preserves sign for A
        A = combined >> 32;
        Q = (uint32_t)combined;
        Q_1 = Q & 1;
    }
    return (A << 32) | (uint32_t)Q;
}

int main() {
    int32_t a = -7, b = 3;
    int64_t res = booth32(a, b);
    cout << "Expected: " << (int64_t)a * b << " Booth-like: " << res << '\n';
}
```

## Assignment 4: Restoring and Non-Restoring Division

**Aim:** Implement restoring and non-restoring division algorithms for binary numbers.

**Theory (expanded):**
- Restoring division subtracts the divisor and, if the partial remainder is negative, restores it and records a 0; otherwise records a 1.
- Non-restoring avoids immediate restore by choosing add/sub based on sign of the running remainder and fixes the final remainder at the end.

**C Example (compact):**
```c
#include <stdio.h>
#include <stdint.h>

uint32_t restoring_div(uint32_t D, uint32_t d, uint32_t *rem) {
    uint64_t A = 0;
    uint64_t Q = D;
    for (int i = 0; i < 32; ++i) {
        A = (A << 1) | ((Q >> 31) & 1);
        Q <<= 1;
        A = A - d;
        if ((int64_t)A < 0) { Q |= 0; A += d; }
        else Q |= 1;
    }
    if (rem) *rem = (uint32_t)A;
    return (uint32_t)Q;
}

int main() {
    uint32_t q, r;
    q = restoring_div(100, 7, &r);
    printf("100 / 7 = %u rem %u\n", q, r);
}
```

## Assignment 5: CPU Scheduling Algorithms

**Aim:** Implement SJF and FCFS; compare average waiting time.

**Theory (expanded):**
- FCFS is simple but can suffer from convoy effect.
- Non-preemptive SJF minimizes average waiting time when burst lengths are known; preemptive SJF (SRTF) can further improve responsiveness.

**C++ Example (FCFS & non-preemptive SJF):**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct P {
    int id, at, bt;
};

void fcfs(const vector<P>& jobs) {
    int t = 0;
    double tw = 0;
    for (auto& p : jobs) {
        if (t < p.at) t = p.at;
        int wt = t - p.at;
        cout << "P" << p.id << " wait=" << wt << "\n";
        tw += wt;
        t += p.bt;
    }
    cout << "Avg=" << tw / jobs.size() << "\n";
}

void sjf(vector<P> jobs) {
    int n = jobs.size(), t = 0, done = 0;
    double tw = 0;
    vector<bool> vis(n);
    while (done < n) {
        int idx = -1, minbt = 1e9;
        for (int i = 0; i < n; i++)
            if (!vis[i] && jobs[i].at <= t && jobs[i].bt < minbt) {
                minbt = jobs[i].bt;
                idx = i;
            }
        if (idx == -1) {
            t++;
            continue;
        }
        int wt = t - jobs[idx].at;
        cout << "P" << jobs[idx].id << " wait=" << wt << "\n";
        tw += wt;
        t += jobs[idx].bt;
        vis[idx] = true;
        done++;
    }
    cout << "Avg=" << tw / n << "\n";
}

int main() {
    vector<P> j = {{1, 0, 10}, {2, 2, 5}, {3, 3, 8}};
    cout << "FCFS\n";
    fcfs(j);
    cout << "SJF\n";
    sjf(j);
}
```

## Assignment 6: Banker's Algorithm

**Aim:** Implement the Banker's algorithm to check for safe state.

**C++ Example (safety check function):**
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool safe(const vector<int>& avail, const vector<vector<int>>& maxm, const vector<vector<int>>& alloc) {
    int n = maxm.size(), m = avail.size();
    vector<int> work = avail;
    vector<bool> fin(n, false);
    for (;;) {
        bool progress = false;
        for (int i = 0; i < n; i++)
            if (!fin[i]) {
                bool ok = true;
                for (int j = 0; j < m; j++)
                    if (maxm[i][j] - alloc[i][j] > work[j]) {
                        ok = false;
                        break;
                    }
                if (ok) {
                    for (int j = 0; j < m; j++) work[j] += alloc[i][j];
                    fin[i] = true;
                    progress = true;
                }
            }
        if (!progress) break;
    }
    for (bool f : fin) if (!f) return false;
    return true;
}

int main() {
    vector<int> avail = {3, 3, 2};
    vector<vector<int>> maxm = {{7, 5, 3}, {3, 2, 2}, {9, 0, 2}, {2, 2, 2}, {4, 3, 3}};
    vector<vector<int>> alloc = {{0, 1, 0}, {2, 0, 0}, {3, 0, 2}, {2, 1, 1}, {0, 0, 2}};
    cout << (safe(avail, maxm, alloc) ? "Safe\n" : "Unsafe\n");
}
```

## Assignment 7: Page Replacement Algorithms

**Aim:** Implement Optimal and LRU page replacement; measure page faults.

**Theory (expanded):**
- Optimal is the lower bound (requires future knowledge).
- LRU uses past usage as a heuristic; implementable with a list or timestamps.

**C++ Examples (compact):**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int lru(const vector<int>& pages, int cap) {
    vector<int> f;
    int faults = 0;
    for (int i = 0; i < pages.size(); ++i) {
        int p = pages[i];
        auto it = find(f.begin(), f.end(), p);
        if (it == f.end()) {
            if (f.size() < cap) f.push_back(p);
            else {
                int lruidx = 0, oldest = 1e9;
                for (int j = 0; j < f.size(); ++j) {
                    int last = -1;
                    for (int k = i - 1; k >= 0; --k)
                        if (pages[k] == f[j]) {
                            last = k;
                            break;
                        }
                    if (last < oldest) {
                        oldest = last;
                        lruidx = j;
                    }
                }
                f[lruidx] = p;
            }
            faults++;
        }
    }
    return faults;
}

int optimal(const vector<int>& pages, int cap) {
    vector<int> f;
    int faults = 0;
    for (int i = 0; i < pages.size(); ++i) {
        int p = pages[i];
        if (find(f.begin(), f.end(), p) == f.end()) {
            if (f.size() < cap) f.push_back(p);
            else {
                int rep = -1, farthest = -1;
                for (int j = 0; j < f.size(); ++j) {
                    int k;
                    for (k = i + 1; k < pages.size() && pages[k] != f[j]; ++k);
                    if (k == pages.size()) {
                        rep = j;
                        break;
                    }
                    if (k > farthest) {
                        farthest = k;
                        rep = j;
                    }
                }
                f[rep] = p;
            }
            faults++;
        }
    }
    return faults;
}

int main() {
    vector<int> pages = {7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2};
    cout << "LRU=" << lru(pages, 3) << " Optimal=" << optimal(pages, 3) << "\n";
}
```

## Assignment 8: Simple Text Editor

**Aim:** Implement a simple line-oriented text editor to practice file I/O and buffers.

**C++ Example (minimal REPL):**
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<string> buf;
    string fname = "test.txt", s;
    ifstream in(fname);
    if (in) {
        while (getline(in, s)) buf.push_back(s);
        in.close();
    }
    cout << "Commands: list | insert <n> <text> | delete <n> | save | quit\n";
    while (true) {
        cout << "> ";
        string cmd;
        if (!(cin >> cmd)) break;
        if (cmd == "list") {
            for (int i = 0; i < buf.size(); ++i)
                cout << i + 1 << ": " << buf[i] << "\n";
        } else if (cmd == "insert") {
            int n;
            cin >> n;
            getline(cin, s);
            if (n <= 0) buf.insert(buf.begin(), s);
            else if (n > buf.size()) buf.push_back(s);
            else buf.insert(buf.begin() + n, s);
        } else if (cmd == "delete") {
            int n;
            cin >> n;
            if (n > 0 && n <= buf.size()) buf.erase(buf.begin() + n - 1);
        } else if (cmd == "save") {
            ofstream out(fname);
            for (auto &l : buf) out << l << "\n";
            out.close();
            cout << "Saved\n";
        } else if (cmd == "quit") break;
    }
}
```

## Assignment 9: Simple File Management System

**Aim:** Implement a basic in-memory file manager supporting mkdir, cd, ls, touch.

**Python Example (in-memory):**
```python
class Node:
    def __init__(self,name,is_dir=True):
        self.name=name
        self.is_dir=is_dir
        self.children={} if is_dir else None

class FS:
    def __init__(self):
        self.root=Node('/')
        self.cwd=self.root
        self.path=[self.root]
    def mkdir(self,name):
        if name not in self.cwd.children: self.cwd.children[name]=Node(name,True)
    def touch(self,name):
        self.cwd.children[name]=Node(name,False)
    def ls(self):
        print(' '.join(sorted(self.cwd.children.keys())))
    def cd(self,name):
        if name=='/': self.cwd=self.root; self.path=[self.root]; return
        if name=='..' and len(self.path)>1: self.path.pop(); self.cwd=self.path[-1]; return
        if name in self.cwd.children and self.cwd.children[name].is_dir: self.cwd=self.cwd.children[name]; self.path.append(self.cwd)

if __name__=='__main__':
    fs=FS(); fs.mkdir('docs'); fs.touch('readme.txt'); fs.ls(); fs.cd('docs'); fs.touch('notes.txt'); fs.cd('..'); fs.ls()
```

## Assignment 10: Linux Commands

**Aim:** Practice common Linux commands and scripting patterns.

**Notes (expanded):**
- Learn file ops (`ls`, `cp`, `mv`, `rm`), process inspection (`ps`, `top`), text tools (`grep`, `sed`, `awk`), and permission bits (`chmod`, `chown`). Combine commands with pipes and redirection for real power.

## Assignment 11: Shell Scripting

**Aim:** Learn to automate tasks with shell scripts.

**Example (bash):**
```bash
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

**Final notes:**
- The snippets above are intentionally compact so you can paste and run them quickly in a local environment. They are educational building blocks: expand input handling, error checks, and tests as next steps.

---

Files changed: `COOS.md` — expanded explanations and added runnable example implementations for each assignment.
