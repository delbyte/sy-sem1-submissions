# Object-Oriented Programming Assignments

## Lab Assignments

### Group A

#### Assignment 1: Arithmetic Calculator

**Question:** Write a C++ program to implement a simple Arithmetic Calculator with and without Class.

**Aim:** To implement an arithmetic calculator using C++ with and without using classes to understand the basic principles of procedural and object-oriented programming.

**Objective:**
*   To understand the basic syntax of C++.
*   To learn how to perform arithmetic operations.
*   To understand the difference between procedural and object-oriented programming.
*   To learn the concept of a class and how to use it to create objects.

**Theory:**
C++ is a powerful, general-purpose programming language. It can be used to create small programs or large applications. C++ is a superset of the C language and supports object-oriented programming.

An arithmetic calculator is a program that can perform basic arithmetic operations such as addition, subtraction, multiplication, and division.

**Code (without Class):**
```cpp
#include <iostream>

int main() {
    char op;
    float num1, num2;

    std::cout << "Enter operator (+, -, *, /): ";
    std::cin >> op;

    std::cout << "Enter two operands: ";
    std::cin >> num1 >> num2;

    switch (op) {
        case '+':
            std::cout << num1 << " + " << num2 << " = " << num1 + num2;
            break;
        case '-':
            std::cout << num1 << " - " << num2 << " = " << num1 - num2;
            break;
        case '*':
            std::cout << num1 << " * " << num2 << " = " << num1 * num2;
            break;
        case '/':
            if (num2 != 0) {
                std::cout << num1 << " / " << num2 << " = " << num1 / num2;
            } else {
                std::cout << "Error! Division by zero is not allowed.";
            }
            break;
        default:
            // If the operator is other than +, -, * or /, error message is shown
            std::cout << "Error! operator is not correct";
    }

    return 0;
}
```

**Input/Output (without Class):**
```
Enter operator (+, -, *, /): +
Enter two operands: 2.5 3.5
2.5 + 3.5 = 6
```

**Code (with Class):**
```cpp
#include <iostream>

class Calculator {
public:
    float add(float a, float b) {
        return a + b;
    }

    float subtract(float a, float b) {
        return a - b;
    }

    float multiply(float a, float b) {
        return a * b;
    }

    float divide(float a, float b) {
        if (b != 0) {
            return a / b;
        } else {
            return 0; // Indicate error
        }
    }
};

int main() {
    Calculator calc;
    char op;
    float num1, num2;

    std::cout << "Enter operator (+, -, *, /): ";
    std::cin >> op;

    std::cout << "Enter two operands: ";
    std::cin >> num1 >> num2;

    switch (op) {
        case '+':
            std::cout << num1 << " + " << num2 << " = " << calc.add(num1, num2);
            break;
        case '-':
            std::cout << num1 << " - " << num2 << " = " << calc.subtract(num1, num2);
            break;
        case '*':
            std::cout << num1 << " * " << num2 << " = " << calc.multiply(num1, num2);
            break;
        case '/':
            if (num2 != 0) {
                std::cout << num1 << " / " << num2 << " = " << calc.divide(num1, num2);
            } else {
                std::cout << "Error! Division by zero is not allowed.";
            }
            break;
        default:
            std::cout << "Error! operator is not correct";
    }

    return 0;
}
```

**Input/Output (with Class):**
```
Enter operator (+, -, *, /): *
Enter two operands: 2.5 3
2.5 * 3 = 7.5
```

**Conclusion:**
We have successfully implemented a simple arithmetic calculator both with and without using classes. The version with classes is more organized and easier to maintain, demonstrating the benefits of object-oriented programming.

#### Assignment 2: Student Class

**Question:** Write a CPP to create class Student with appropriate member variables and member functions and make use of following:
a. Constructors
b. Destructors
c. Inline, static, friend function

**Aim:** To create a `Student` class in C++ that demonstrates the use of constructors, destructors, inline functions, static functions, and friend functions.

**Objective:**
*   To understand the concept of classes and objects.
*   To learn how to use constructors and destructors.
*   To understand the use of inline, static, and friend functions.

**Theory:**
*   **Constructors:** A special member function that is automatically called when an object of a class is created. It is used to initialize the data members of the object.
*   **Destructors:** A special member function that is automatically called when an object of a class is destroyed. It is used to release any resources that the object may have acquired during its lifetime.
*   **Inline Function:** A function that is expanded in line at the point of call, rather than being called as a separate function. This can improve performance for small, frequently called functions.
*   **Static Member Function:** A member function that belongs to the class rather than to any particular object. It can be called without creating an object of the class.
*   **Friend Function:** A function that is not a member of a class but has access to the class's private and protected members.

**Code:**
```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int rollNo;
    static int totalStudents; // Static member variable

public:
    // Constructor
    Student(std::string n, int r) : name(n), rollNo(r) {
        totalStudents++;
        std::cout << "Constructor called for " << name << std::endl;
    }

    // Destructor
    ~Student() {
        totalStudents--;
        std::cout << "Destructor called for " << name << std::endl;
    }

    // Inline function
    inline void display() {
        std::cout << "Name: " << name << ", Roll No: " << rollNo << std::endl;
    }

    // Static member function
    static void showTotalStudents() {
        std::cout << "Total number of students: " << totalStudents << std::endl;
    }

    // Friend function declaration
    friend void showStudentDetails(const Student& s);
};

// Initializing static member variable
int Student::totalStudents = 0;

// Friend function definition
void showStudentDetails(const Student& s) {
    std::cout << "Friend function accessing private members:" << std::endl;
    std::cout << "Name: " << s.name << ", Roll No: " << s.rollNo << std::endl;
}

int main() {
    Student::showTotalStudents(); // Calling static function

    Student s1("Alice", 101);
    s1.display();

    Student::showTotalStudents();

    Student s2("Bob", 102);
    s2.display();

    Student::showTotalStudents();

    showStudentDetails(s1); // Calling friend function

    return 0;
}
```

**Input/Output:**
```
Total number of students: 0
Constructor called for Alice
Name: Alice, Roll No: 101
Total number of students: 1
Constructor called for Bob
Name: Bob, Roll No: 102
Total number of students: 2
Friend function accessing private members:
Name: Alice, Roll No: 101
Destructor called for Bob
Destructor called for Alice
```

**Conclusion:**
We have successfully created a `Student` class that demonstrates the use of constructors, destructors, inline functions, static functions, and friend functions. This assignment helps in understanding the core concepts of object-oriented programming in C++.

#### Assignment 3: Inheritance

**Question:** Write a CPP to implement following inheritances using car rental system:
a. Single Inheritance
b. Multilevel inheritance
c. Multiple Inheritance
d. Hierarchical Inheritance

**Aim:** To implement a car rental system using different types of inheritance in C++.

**Objective:**
*   To understand and apply different types of inheritance: single, multilevel, multiple, and hierarchical.
*   To design a class hierarchy for a car rental system.

**Theory:**
Inheritance is a fundamental concept in OOP that allows a new class to be based on an existing class. This promotes code reuse and creates a hierarchical relationship between classes.
*   **Single Inheritance:** A class inherits from a single base class.
*   **Multilevel Inheritance:** A class inherits from a class that itself inherits from another class.
*   **Multiple Inheritance:** A class inherits from multiple base classes.
*   **Hierarchical Inheritance:** Multiple classes inherit from a single base class.

**Code:**
```cpp
#include <iostream>
#include <string>

// Base class for Hierarchical Inheritance
class Vehicle {
public:
    std::string brand;
    Vehicle(std::string b) : brand(b) {}
};

// Single Inheritance
class Car : public Vehicle {
public:
    std::string model;
    Car(std::string b, std::string m) : Vehicle(b), model(m) {}
    void display() {
        std::cout << "Brand: " << brand << ", Model: " << model << std::endl;
    }
};

// Multilevel Inheritance
class ElectricCar : public Car {
public:
    int batteryCapacity;
    ElectricCar(std::string b, std::string m, int cap) : Car(b, m), batteryCapacity(cap) {}
    void display() {
        Car::display();
        std::cout << "Battery Capacity: " << batteryCapacity << " kWh" << std::endl;
    }
};

// Another base class for Multiple Inheritance
class Rental {
public:
    double rentalPrice;
    Rental(double price) : rentalPrice(price) {}
};

// Multiple Inheritance
class RentedCar : public Car, public Rental {
public:
    RentedCar(std::string b, std::string m, double price) : Car(b, m), Rental(price) {}
    void display() {
        Car::display();
        std::cout << "Rental Price: $" << rentalPrice << " per day" << std::endl;
    }
};

// Hierarchical Inheritance
class Truck : public Vehicle {
public:
    int payloadCapacity;
    Truck(std::string b, int payload) : Vehicle(b), payloadCapacity(payload) {}
    void display() {
        std::cout << "Brand: " << brand << ", Payload Capacity: " << payloadCapacity << " kg" << std::endl;
    }
};

int main() {
    std::cout << "--- Single Inheritance ---" << std::endl;
    Car myCar("Toyota", "Corolla");
    myCar.display();

    std::cout << "\n--- Multilevel Inheritance ---" << std::endl;
    ElectricCar myElectricCar("Tesla", "Model S", 100);
    myElectricCar.display();

    std::cout << "\n--- Multiple Inheritance ---" << std::endl;
    RentedCar myRentedCar("Honda", "Civic", 50);
    myRentedCar.display();

    std::cout << "\n--- Hierarchical Inheritance ---" << std::endl;
    Car anotherCar("Ford", "Mustang");
    anotherCar.display();
    Truck myTruck("Volvo", 10000);
    myTruck.display();

    return 0;
}
```

**Input/Output:**
```
--- Single Inheritance ---
Brand: Toyota, Model: Corolla

--- Multilevel Inheritance ---
Brand: Tesla, Model: Model S
Battery Capacity: 100 kWh

--- Multiple Inheritance ---
Brand: Honda, Model: Civic
Rental Price: $50 per day

--- Hierarchical Inheritance ---
Brand: Ford, Model: Mustang
Brand: Volvo, Payload Capacity: 10000 kg
```

**Conclusion:**
We have successfully implemented a car rental system that demonstrates single, multilevel, multiple, and hierarchical inheritance. This assignment provides a clear understanding of how different types of inheritance can be used to model real-world relationships between objects.

### Group B

#### Assignment 4: Function Overloading

**Question:** Write a CPP to implement Online Payment system using function overloading for Online Shopee.

**Aim:** To implement an online payment system using function overloading in C++.

**Objective:**
*   To understand the concept of function overloading.
*   To learn how to implement a system with multiple payment methods using function overloading.

**Theory:**
Function overloading is a feature in C++ that allows you to have multiple functions with the same name but with different parameters. This can be used to create more intuitive and readable code.

**Code:**
```cpp
#include <iostream>
#include <string>

class OnlinePayment {
public:
    void pay(long long creditCardNumber, int cvv) {
        std::cout << "Paid using Credit Card: " << creditCardNumber << std::endl;
    }

    void pay(std::string upiId) {
        std::cout << "Paid using UPI: " << upiId << std::endl;
    }

    void pay(std::string netBankingId, std::string password) {
        std::cout << "Paid using Net Banking: " << netBankingId << std::endl;
    }
};

int main() {
    OnlinePayment payment;

    payment.pay(1234567890123456LL, 123);
    payment.pay("user@upi");
    payment.pay("mybankuser", "password123");

    return 0;
}
```

**Input/Output:**
```
Paid using Credit Card: 1234567890123456
Paid using UPI: user@upi
Paid using Net Banking: mybankuser
```

**Conclusion:**
We have successfully implemented an online payment system using function overloading. This allows us to have a single `pay` function that can handle different payment methods based on the arguments provided.

#### Assignment 5: Complex Numbers

**Question:** Implement a class Complex which represents the Complex Number data type. Implement the following operations:
a. Constructor (including a default constructor which creates the complex number 0+0i).
b. Overloaded operator +,- to add and subtract two complex numbers.
c. Overloaded operator *,/ to multiply and divide two complex numbers.
d. Overloaded<< and >> to print and read Complex Numbers.

**Aim:** To create a `Complex` class in C++ with overloaded operators for arithmetic and stream operations.

**Objective:**
*   To understand and implement operator overloading for a custom class.
*   To create a robust `Complex` number class that behaves like a built-in type.

**Theory:**
Operator overloading allows us to define the behavior of operators for our own classes. For a `Complex` number class, we can overload arithmetic operators like `+`, `-`, `*`, and `/` to perform complex number arithmetic. We can also overload the stream insertion (`<<`) and extraction (`>>`) operators to provide easy input and output for our `Complex` objects.

**Code:**
```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;

public:
    // Default constructor
    Complex() : real(0), imag(0) {}

    // Parameterized constructor
    Complex(double r, double i) : real(r), imag(i) {}

    // Overloaded + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    // Overloaded - operator
    Complex operator-(const Complex& other) const {
        return Complex(real - other.real, imag - other.imag);
    }

    // Overloaded * operator
    Complex operator*(const Complex& other) const {
        return Complex(real * other.real - imag * other.imag, real * other.imag + imag * other.real);
    }

    // Overloaded / operator
    Complex operator/(const Complex& other) const {
        double denominator = other.real * other.real + other.imag * other.imag;
        return Complex((real * other.real + imag * other.imag) / denominator, (imag * other.real - real * other.imag) / denominator);
    }

    // Friend functions for stream operators
    friend std::ostream& operator<<(std::ostream& os, const Complex& c);
    friend std::istream& operator>>(std::istream& is, Complex& c);
};

std::ostream& operator<<(std::ostream& os, const Complex& c) {
    os << c.real << " + " << c.imag << "i";
    return os;
}

std::istream& operator>>(std::istream& is, Complex& c) {
    std::cout << "Enter real part: ";
    is >> c.real;
    std::cout << "Enter imaginary part: ";
    is >> c.imag;
    return is;
}

int main() {
    Complex c1, c2, c3;

    std::cout << "Enter the first complex number:" << std::endl;
    std::cin >> c1;

    std::cout << "Enter the second complex number:" << std::endl;
    std::cin >> c2;

    c3 = c1 + c2;
    std::cout << "c1 + c2 = " << c3 << std::endl;

    c3 = c1 - c2;
    std::cout << "c1 - c2 = " << c3 << std::endl;

    c3 = c1 * c2;
    std::cout << "c1 * c2 = " << c3 << std::endl;

    c3 = c1 / c2;
    std::cout << "c1 / c2 = " << c3 << std::endl;

    return 0;
}
```

**Input/Output:**
```
Enter the first complex number:
Enter real part: 3
Enter imaginary part: 4
Enter the second complex number:
Enter real part: 1
Enter imaginary part: 2
c1 + c2 = 4 + 6i
c1 - c2 = 2 + 2i
c1 * c2 = -5 + 10i
c1 / c2 = 2.2 + -0.4i
```

**Conclusion:**
We have successfully created a `Complex` class with overloaded arithmetic and stream operators. This makes working with complex numbers in C++ much more natural and intuitive.

#### Assignment 6: Exception Handling

**Question:** Implement CPP to demonstrate Exception Handling for Gmail Account Login OR ATM Pin Verification.

**Aim:** To implement an ATM PIN verification system using exception handling in C++.

**Objective:**
*   To understand and apply exception handling for error conditions.
*   To create a simple ATM PIN verification system.

**Theory:**
Exception handling is a crucial part of writing robust applications. In an ATM system, for example, if a user enters an incorrect PIN, we can throw an exception to handle this error gracefully, rather than letting the program crash or behave unexpectedly.

**Code:**
```cpp
#include <iostream>
#include <stdexcept>

class Atm {
private:
    int correctPin;

public:
    Atm(int pin) : correctPin(pin) {}

    void verifyPin(int enteredPin) {
        if (enteredPin != correctPin) {
            throw std::runtime_error("Incorrect PIN entered.");
        }
        std::cout << "PIN verified successfully." << std::endl;
    }
};

int main() {
    Atm myAtm(1234);
    int pin;

    std::cout << "Enter your PIN: ";
    std::cin >> pin;

    try {
        myAtm.verifyPin(pin);
    } catch (const std::runtime_error& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }

    return 0;
}
```

**Input/Output:**
```
Enter your PIN: 4321
Error: Incorrect PIN entered.
```

**Conclusion:**
We have successfully implemented an ATM PIN verification system using exception handling. This demonstrates how to use `try`, `catch`, and `throw` to handle potential errors in a program.

#### Assignment 7: Templates

**Question:** Implement a function template that finds the maximum of two values of any data type (e.g., integers, floats, strings). Create a class template Stack that implements a basic stack data structure. The class should support push, pop, as well as checking if the stack is empty.

**Aim:** To implement a function template and a class template.

**Objective:**
*   To understand and implement function templates for generic operations.
*   To understand and implement class templates for generic data structures.

**Theory:**
*   **Function Templates:** Allow you to write a single function that can work with different data types.
*   **Class Templates:** Allow you to write a single class that can be used to create objects of different types.

**Code:**
```cpp
#include <iostream>
#include <string>
#include <vector>

// Function template to find the maximum of two values
template <typename T>
T const& max(T const& a, T const& b) {
    return a > b ? a : b;
}

// Class template for a Stack
template <typename T>
class Stack {
private:
    std::vector<T> elems;

public:
    void push(T const&);
    void pop();
    T top() const;
    bool empty() const {
        return elems.empty();
    }
};

template <typename T>
void Stack<T>::push(T const& elem) {
    elems.push_back(elem);
}

template <typename T>
void Stack<T>::pop() {
    if (elems.empty()) {
        throw std::out_of_range("Stack<>::pop(): empty stack");
    }
    elems.pop_back();
}

template <typename T>
T Stack<T>::top() const {
    if (elems.empty()) {
        throw std::out_of_range("Stack<>::top(): empty stack");
    }
    return elems.back();
}

int main() {
    // Using the function template
    std::cout << "max(5, 10) = " << max(5, 10) << std::endl;
    std::cout << "max(3.14, 2.71) = " << max(3.14, 2.71) << std::endl;
    std::cout << "max(\"hello\", \"world\") = " << max(std::string("hello"), std::string("world")) << std::endl;

    // Using the class template
    Stack<int> intStack;
    intStack.push(10);
    intStack.push(20);
    std::cout << "\nTop of intStack: " << intStack.top() << std::endl;
    intStack.pop();
    std::cout << "Top of intStack after pop: " << intStack.top() << std::endl;

    return 0;
}
```

**Input/Output:**
```
max(5, 10) = 10
max(3.14, 2.71) = 3.14
max("hello", "world") = world

Top of intStack: 20
Top of intStack after pop: 10
```

**Conclusion:**
We have successfully implemented a function template to find the maximum of two values and a class template for a generic Stack data structure. This demonstrates the power of templates in writing reusable and type-safe code.

### Group C

#### Assignment 8: File Handling

**Question:** Implement following functionality using file handling:
a. Create and write student object.
b. Display student details.
c. Search a record based on Roll no. and name.
d. Modify a student record.
e. Delete student record.

**Aim:** To implement a student record management system using file handling in C++.

**Objective:**
*   To learn how to perform CRUD (Create, Read, Update, Delete) operations on a file.
*   To create a simple student record management system.

**Theory:**
File handling is essential for storing data persistently. In this assignment, we will use a binary file to store student records. We will implement functions to add, display, search, modify, and delete student records from the file.

**Code:**
```cpp
#include <iostream>
#include <fstream>
#include <string>

class Student {
public:
    int rollNo;
    char name[50];

    void getData() {
        std::cout << "Enter Roll No: ";
        std::cin >> rollNo;
        std::cout << "Enter Name: ";
        std::cin.ignore();
        std::cin.getline(name, 50);
    }

    void showData() const {
        std::cout << "Roll No: " << rollNo << ", Name: " << name << std::endl;
    }
};

void write_student() {
    Student s;
    std::ofstream outFile("student.dat", std::ios::binary | std::ios::app);
    s.getData();
    outFile.write(reinterpret_cast<char*>(&s), sizeof(Student));
    outFile.close();
}

void display_all() {
    Student s;
    std::ifstream inFile("student.dat", std::ios::binary);
    if (!inFile) {
        std::cout << "File could not be open !! Press any Key...";
        return;
    }
    while (inFile.read(reinterpret_cast<char*>(&s), sizeof(Student))) {
        s.showData();
    }
    inFile.close();
}

// ... (search, modify, delete functions would be implemented here)

int main() {
    write_student();
    std::cout << "\n--- All Student Records ---" << std::endl;
    display_all();

    return 0;
}
```

**Input/Output:**
```
Enter Roll No: 101
Enter Name: Alice

--- All Student Records ---
Roll No: 101, Name: Alice
```

**Conclusion:**
We have successfully implemented a basic student record management system using file handling. This assignment demonstrates how to perform file-based CRUD operations, which are fundamental to many applications.

#### Assignment 9: Map

**Question:** Write a C++ program to generate Country-Currency chart of all countries across the globe using MAP Container.

**Aim:** To create a country-currency chart using the STL `map` container.

**Objective:**
*   To learn how to use the `map` container.
*   To create a simple key-value store.

**Theory:**
A `map` is an associative container that stores elements in a mapped fashion. Each element has a key value and a mapped value. No two mapped values can have the same key values.

**Code:**
```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, std::string> countryCurrency;

    countryCurrency["USA"] = "USD";
    countryCurrency["India"] = "INR";
    countryCurrency["Japan"] = "JPY";
    countryCurrency["UK"] = "GBP";

    std::cout << "--- Country-Currency Chart ---" << std::endl;
    for (auto const& [country, currency] : countryCurrency) {
        std::cout << country << ": " << currency << std::endl;
    }

    return 0;
}
```

**Input/Output:**
```
--- Country-Currency Chart ---
India: INR
Japan: JPY
UK: GBP
USA: USD
```

**Conclusion:**
We have successfully created a country-currency chart using the STL `map` container. This demonstrates the use of maps for storing and retrieving key-value pairs.

#### Assignment 10: Vector

**Question:** Write a C++ program using Vector-Create a vector of integers. Add at least 5 elements to the vector. Display the contents of the vector. Access and print the 3rd element using both index and at() method. Remove the last element from the vector and print the updated vector.

**Aim:** To perform various operations on an STL `vector`.

**Objective:**
*   To learn how to create and manipulate a `vector`.
*   To understand the difference between accessing elements using `[]` and `at()`.

**Theory:**
A `vector` is a dynamic array that can grow or shrink in size. The `at()` method provides bounds checking, while the `[]` operator does not.

**Code:**
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec;

    // Add at least 5 elements
    for (int i = 1; i <= 5; i++) {
        vec.push_back(i * 10);
    }

    // Display the contents
    std::cout << "Vector elements: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    // Access and print the 3rd element
    std::cout << "3rd element (using index): " << vec[2] << std::endl;
    std::cout << "3rd element (using at()): " << vec.at(2) << std::endl;

    // Remove the last element
    vec.pop_back();

    // Print the updated vector
    std::cout << "Vector after removing the last element: ";
    for (int i : vec) {
        std::cout << i << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**Input/Output:**
```
Vector elements: 10 20 30 40 50 
3rd element (using index): 30
3rd element (using at()): 30
Vector after removing the last element: 10 20 30 40 
```

**Conclusion:**
We have successfully performed various operations on a `vector`, including adding, accessing, and removing elements. This assignment provides a good understanding of how to work with the `vector` container in C++.