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

## Theory Assignments

### Assignment 1: OOP Features and Basic C++ Concepts

**Question 1:** Explain features of OOP: Encapsulation, Inheritance, Abstraction, Polymorphism, data hiding, class and object.

**Aim:** To understand and explain the fundamental features of Object-Oriented Programming (OOP).

**Objective:** To define and provide examples for Encapsulation, Inheritance, Abstraction, Polymorphism, Data Hiding, Class, and Object.

**Theory:**

*   **Encapsulation:** The bundling of data (attributes) and methods (functions) that operate on the data into a single unit called a class. It restricts direct access to some of an object's components, which is a means of preventing accidental interference and misuse of the data.
*   **Inheritance:** A mechanism in which one class acquires the properties (attributes and methods) of another class. The class that inherits the properties is called the derived or child class, and the class whose properties are inherited is called the base or parent class.
*   **Abstraction:** The concept of hiding the complex implementation details and showing only the essential features of the object. It helps in managing complexity by allowing us to focus on what an object does instead of how it does it.
*   **Polymorphism:** The ability of a message to be displayed in more than one form. It allows us to perform a single action in different ways. For example, a single `draw()` method can be used to draw different shapes like a circle, a square, or a rectangle.
*   **Data Hiding:** A mechanism of restricting access to the data members of a class. This is typically achieved by declaring the data members as private.
*   **Class:** A blueprint for creating objects. It is a user-defined data type that holds its own data members and member functions, which can be accessed and used by creating an instance of that class.
*   **Object:** An instance of a class. When a class is defined, no memory is allocated, but when it is instantiated (an object is created), memory is allocated.

**Conclusion:** Understanding these fundamental concepts is crucial for developing robust and maintainable software using the object-oriented paradigm.

**Question 2:** Write a program demonstrating inline function, static function, friend function, constructor and destructor.

**Aim:** To write a C++ program that demonstrates the use of inline functions, static functions, friend functions, constructors, and destructors.

**Objective:** To practically implement the concepts of inline, static, and friend functions, as well as constructors and destructors in a single C++ program.

**Theory:** See the theory section of Lab Assignment 2.

**Code:** See the code section of Lab Assignment 2.

**Conclusion:** The program successfully demonstrates the implementation and usage of these important C++ features, which are essential for effective object-oriented programming.

### Assignment 2: Inheritance

**Question:** Apply appropriate inheritance type to implement any one of the following problem statement:
1. Banking System
2. Hospital management system
3. Library management system
... (and others)

**Aim:** To implement a banking system using inheritance in C++.

**Objective:**
*   To understand and apply the concept of inheritance.
*   To design a class hierarchy for a banking system.
*   To implement different types of accounts (e.g., Savings, Checking) that inherit from a base `Account` class.

**Theory:**
Inheritance is a fundamental concept in OOP that allows a new class to be based on an existing class. The new class inherits the properties and behavior of the existing class. This promotes code reuse and creates a hierarchical relationship between classes.

For a banking system, we can have a base `Account` class with common attributes like account number and balance, and common methods like `deposit()` and `withdraw()`. Then, we can create specialized account types like `SavingsAccount` and `CheckingAccount` that inherit from the `Account` class and add their own specific features (e.g., interest calculation for savings, overdraft protection for checking).

**Code:**
```cpp
#include <iostream>
#include <string>

// Base class
class Account {
protected:
    std::string accountNumber;
    double balance;

public:
    Account(std::string accNum, double bal) : accountNumber(accNum), balance(bal) {}

    void deposit(double amount) {
        balance += amount;
        std::cout << "Deposited " << amount << ". New balance: " << balance << std::endl;
    }

    virtual void withdraw(double amount) {
        if (balance >= amount) {
            balance -= amount;
            std::cout << "Withdrew " << amount << ". New balance: " << balance << std::endl;
        } else {
            std::cout << "Insufficient balance." << std::endl;
        }
    }

    void display() {
        std::cout << "Account Number: " << accountNumber << ", Balance: " << balance << std::endl;
    }
};

// Derived class
class SavingsAccount : public Account {
private:
    double interestRate;

public:
    SavingsAccount(std::string accNum, double bal, double rate) : Account(accNum, bal), interestRate(rate) {}

    void addInterest() {
        double interest = balance * interestRate;
        deposit(interest);
    }
};

// Derived class
class CheckingAccount : public Account {
private:
    double overdraftLimit;

public:
    CheckingAccount(std::string accNum, double bal, double limit) : Account(accNum, bal), overdraftLimit(limit) {}

    void withdraw(double amount) override {
        if (balance + overdraftLimit >= amount) {
            balance -= amount;
            std::cout << "Withdrew " << amount << ". New balance: " << balance << std::endl;
        } else {
            std::cout << "Overdraft limit exceeded." << std::endl;
        }
    }
};

int main() {
    SavingsAccount sa("SA123", 1000, 0.05);
    sa.display();
    sa.deposit(500);
    sa.addInterest();
    sa.display();

    std::cout << std::endl;

    CheckingAccount ca("CA456", 2000, 500);
    ca.display();
    ca.withdraw(2200);
    ca.display();
    ca.withdraw(400);

    return 0;
}
```

**Input/Output:**
```
Account Number: SA123, Balance: 1000
Deposited 500. New balance: 1500
Deposited 75. New balance: 1575
Account Number: SA123, Balance: 1575

Account Number: CA456, Balance: 2000
Withdrew 2200. New balance: -200
Account Number: CA456, Balance: -200
Overdraft limit exceeded.
```

**Conclusion:**
We have successfully implemented a simple banking system using inheritance. The `SavingsAccount` and `CheckingAccount` classes inherit from the `Account` class, demonstrating code reuse and the power of inheritance in creating a well-structured and extensible system.

### Assignment 3: Operator Overloading and Virtual Functions

**Question 1:** Implement operator overloading (Binary and Unary).

**Aim:** To implement binary and unary operator overloading in C++.

**Objective:**
*   To understand the concept of operator overloading.
*   To learn how to overload binary and unary operators.

**Theory:**
Operator overloading is a feature in C++ that allows programmers to redefine the behavior of operators for user-defined types (classes). This can make the code more intuitive and readable.

*   **Unary Operator Overloading:** Overloading an operator that takes one operand (e.g., `++`, `--`, `-`).
*   **Binary Operator Overloading:** Overloading an operator that takes two operands (e.g., `+`, `-`, `*`, `/`).

**Code:**
```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;

public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // Overloading the binary + operator
    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }

    // Overloading the unary - operator
    Complex operator-() {
        return Complex(-real, -imag);
    }

    void display() {
        std::cout << real << " + " << imag << "i" << std::endl;
    }
};

int main() {
    Complex c1(3, 4);
    Complex c2(1, 2);
    Complex c3 = c1 + c2; // Binary operator overloading

    std::cout << "c1 = ";
    c1.display();
    std::cout << "c2 = ";
    c2.display();
    std::cout << "c3 = c1 + c2 = ";
    c3.display();

    Complex c4 = -c1; // Unary operator overloading
    std::cout << "c4 = -c1 = ";
    c4.display();

    return 0;
}
```

**Input/Output:**
```
c1 = 3 + 4i
c2 = 1 + 2i
c3 = c1 + c2 = 4 + 6i
c4 = -c1 = -3 + -4i
```

**Conclusion:**
We have successfully implemented operator overloading for both binary and unary operators. This allows us to use standard operators with our custom `Complex` class, making the code more readable and intuitive.

**Question 2:** Implement virtual function and pure virtual function.

**Aim:** To implement virtual and pure virtual functions in C++.

**Objective:**
*   To understand the concept of virtual functions and runtime polymorphism.
*   To learn how to use pure virtual functions to create abstract classes.

**Theory:**
*   **Virtual Function:** A member function that is declared within a base class and is re-defined (overridden) by a derived class. When you refer to a derived class object using a pointer or a reference to the base class, you can call a virtual function for that object and execute the derived class's version of the function.
*   **Pure Virtual Function:** A virtual function for which we don't have an implementation. We only declare it. A pure virtual function is declared by assigning 0 in the declaration. A class that has at least one pure virtual function is called an abstract class.

**Code:**
```cpp
#include <iostream>

// Abstract base class
class Shape {
public:
    // Pure virtual function
    virtual float calculateArea() = 0;
};

class Square : public Shape {
private:
    float side;

public:
    Square(float s) : side(s) {}

    float calculateArea() override {
        return side * side;
    }
};

class Circle : public Shape {
private:
    float radius;

public:
    Circle(float r) : radius(r) {}

    float calculateArea() override {
        return 3.14159 * radius * radius;
    }
};

int main() {
    Shape* shape;
    Square s(5);
    Circle c(3);

    shape = &s;
    std::cout << "Area of square: " << shape->calculateArea() << std::endl;

    shape = &c;
    std::cout << "Area of circle: " << shape->calculateArea() << std::endl;

    return 0;
}
```

**Input/Output:**
```
Area of square: 25
Area of circle: 28.2743
```

**Conclusion:**
We have successfully implemented virtual and pure virtual functions. The `Shape` class is an abstract class with a pure virtual function `calculateArea()`. The `Square` and `Circle` classes inherit from `Shape` and provide their own implementations for `calculateArea()`, demonstrating runtime polymorphism.

### Assignment 4: Templates

**Question 1:** Write C++ code for function template sorting of values (Number/Characters).

**Aim:** To write a C++ function template for sorting an array of any data type.

**Objective:**
*   To understand the concept of function templates.
*   To learn how to write a generic sorting function that can work with different data types.

**Theory:**
Function templates are a powerful feature in C++ that allow you to write generic functions that can work with different data types. You create a function template by using the `template` keyword.

**Code:**
```cpp
#include <iostream>

template <typename T>
void sort(T arr[], int size) {
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                T temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

template <typename T>
void printArray(T arr[], int size) {
    for (int i = 0; i < size; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int intArr[] = {5, 2, 8, 1, 9};
    char charArr[] = {'d', 'a', 'c', 'b', 'e'};

    std::cout << "Original integer array: ";
    printArray(intArr, 5);
    sort(intArr, 5);
    std::cout << "Sorted integer array: ";
    printArray(intArr, 5);

    std::cout << "\nOriginal character array: ";
    printArray(charArr, 5);
    sort(charArr, 5);
    std::cout << "Sorted character array: ";
    printArray(charArr, 5);

    return 0;
}
```

**Input/Output:**
```
Original integer array: 5 2 8 1 9 
Sorted integer array: 1 2 5 8 9 

Original character array: d a c b e 
Sorted character array: a b c d e 
```

**Conclusion:**
We have successfully created a function template for sorting that can be used with different data types like integers and characters. This demonstrates the power and flexibility of templates in C++.

**Question 2:** Write C++ code for class template: Number class (int/float) supporting arithmetic operations.

**Aim:** To write a C++ class template for a `Number` class that can work with both `int` and `float` types and support basic arithmetic operations.

**Objective:**
*   To understand the concept of class templates.
*   To learn how to create a generic class that can be used with different data types.

**Theory:**
Class templates allow you to create generic classes. You can create a class template for a `Number` class that can be used to create objects that hold numbers of different types (e.g., `int`, `float`, `double`).

**Code:**
```cpp
#include <iostream>

template <typename T>
class Number {
private:
    T value;

public:
    Number(T val) : value(val) {}

    T getValue() const {
        return value;
    }

    Number<T> operator+(const Number<T>& other) const {
        return Number<T>(value + other.value);
    }

    Number<T> operator-(const Number<T>& other) const {
        return Number<T>(value - other.value);
    }

    Number<T> operator*(const Number<T>& other) const {
        return Number<T>(value * other.value);
    }

    Number<T> operator/(const Number<T>& other) const {
        return Number<T>(value / other.value);
    }
};

int main() {
    Number<int> int1(10);
    Number<int> int2(5);

    std::cout << "Integer operations:" << std::endl;
    std::cout << "int1 + int2 = " << (int1 + int2).getValue() << std::endl;
    std::cout << "int1 - int2 = " << (int1 - int2).getValue() << std::endl;
    std::cout << "int1 * int2 = " << (int1 * int2).getValue() << std::endl;
    std::cout << "int1 / int2 = " << (int1 / int2).getValue() << std::endl;

    std::cout << std::endl;

    Number<float> float1(10.5f);
    Number<float> float2(2.5f);

    std::cout << "Float operations:" << std::endl;
    std::cout << "float1 + float2 = " << (float1 + float2).getValue() << std::endl;
    std::cout << "float1 - float2 = " << (float1 - float2).getValue() << std::endl;
    std::cout << "float1 * float2 = " << (float1 * float2).getValue() << std::endl;
    std::cout << "float1 / float2 = " << (float1 / float2).getValue() << std::endl;

    return 0;
}
```

**Input/Output:**
```
Integer operations:
int1 + int2 = 15
int1 - int2 = 5
int1 * int2 = 50
int1 / int2 = 2

Float operations:
float1 + float2 = 13
float1 - float2 = 8
float1 * float2 = 26.25
float1 / float2 = 4.2
```

**Conclusion:**
We have successfully created a class template for a `Number` class that can perform arithmetic operations on different numeric types. This demonstrates the reusability and type safety provided by class templates.

### Assignment 5: File Handling

**Question 1:** Write C++ code to open file.

i) Using constructor and open function
ii) Read no of characters in file
iii) Read first line in file
iv) Read last line in file.

**Aim:** To write a C++ program that demonstrates various file handling operations.

**Objective:**
*   To learn how to open and close files in C++.
*   To read data from a file character by character, line by line.

**Theory:**
C++ provides a rich set of classes for file handling in the `<fstream>` header. The main classes are `ifstream` (for reading from files), `ofstream` (for writing to files), and `fstream` (for both reading and writing).

**Code:**
```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    // Create and write to a file
    std::ofstream outFile("test.txt");
    outFile << "This is the first line.\n";
    outFile << "This is the second line.\n";
    outFile << "This is the last line.\n";
    outFile.close();

    // i) Open file using constructor and open function
    std::ifstream inFile1("test.txt"); // Using constructor
    if (inFile1.is_open()) {
        std::cout << "File opened successfully using constructor." << std::endl;
        inFile1.close();
    }

    std::ifstream inFile2;
    inFile2.open("test.txt"); // Using open function
    if (inFile2.is_open()) {
        std::cout << "File opened successfully using open function." << std::endl;

        // ii) Read number of characters in file
        char ch;
        int count = 0;
        while (inFile2.get(ch)) {
            count++;
        }
        std::cout << "Number of characters in file: " << count << std::endl;
        inFile2.close();
    }

    // iii) Read first line in file
    std::ifstream inFile3("test.txt");
    if (inFile3.is_open()) {
        std::string line;
        std::getline(inFile3, line);
        std::cout << "First line of file: " << line << std::endl;
        inFile3.close();
    }

    // iv) Read last line in file
    std::ifstream inFile4("test.txt");
    if (inFile4.is_open()) {
        std::string line;
        std::string lastLine;
        while (std::getline(inFile4, line)) {
            lastLine = line;
        }
        std::cout << "Last line of file: " << lastLine << std::endl;
        inFile4.close();
    }

    return 0;
}
```

**Input/Output:**
```
File opened successfully using constructor.
File opened successfully using open function.
Number of characters in file: 69
First line of file: This is the first line.
Last line of file: This is the last line.
```

**Conclusion:**
We have successfully demonstrated various file handling operations in C++, including opening files using different methods and reading data from them in different ways.

**Question 2:** Write C++ code for operation using Binary file.

**Aim:** To write a C++ program that performs read and write operations on a binary file.

**Objective:**
*   To understand the difference between text and binary files.
*   To learn how to read and write data to a binary file.

**Theory:**
Binary files store data in the same format as it is stored in memory. This can be more efficient for storing complex data structures. The `fstream` library provides the `ios::binary` flag to open a file in binary mode.

**Code:**
```cpp
#include <iostream>
#include <fstream>

struct Person {
    char name[50];
    int age;
};

int main() {
    Person p1 = {"Alice", 30};
    Person p2;

    // Write to a binary file
    std::ofstream outFile("person.bin", std::ios::binary);
    outFile.write(reinterpret_cast<char*>(&p1), sizeof(Person));
    outFile.close();

    // Read from a binary file
    std::ifstream inFile("person.bin", std::ios::binary);
    inFile.read(reinterpret_cast<char*>(&p2), sizeof(Person));
    inFile.close();

    std::cout << "Data read from binary file:" << std::endl;
    std::cout << "Name: " << p2.name << ", Age: " << p2.age << std::endl;

    return 0;
}
```

**Input/Output:**
```
Data read from binary file:
Name: Alice, Age: 30
```

**Conclusion:**
We have successfully demonstrated how to read and write data to a binary file in C++. This is a useful technique for storing and retrieving complex data structures efficiently.

### Assignment 6: Standard Template Library (STL)

**Question 1:** Write C++ code for STL using Vector operations.

**Aim:** To write a C++ program that demonstrates the use of the STL `vector` container.

**Objective:**
*   To understand the concept of the Standard Template Library (STL).
*   To learn how to use the `vector` container and its various member functions.

**Theory:**
The Standard Template Library (STL) is a set of C++ template classes to provide common programming data structures and functions such as lists, stacks, arrays, etc. It is a library of container classes, algorithms, and iterators. A `vector` is a dynamic array that can grow or shrink in size as needed.

**Code:**
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec;

    // Add elements to the vector
    for (int i = 1; i <= 5; i++) {
        vec.push_back(i);
    }

    // Display the contents of the vector
    std::cout << "Vector elements: ";
    for (int i = 0; i < vec.size(); i++) {
        std::cout << vec[i] << " ";
    }
    std::cout << std::endl;

    // Access and print the 3rd element
    std::cout << "The 3rd element is: " << vec.at(2) << std::endl;

    // Remove the last element
    vec.pop_back();

    // Display the updated vector
    std::cout << "Vector after removing the last element: ";
    for (int i = 0; i < vec.size(); i++) {
        std::cout << vec[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**Input/Output:**
```
Vector elements: 1 2 3 4 5 
The 3rd element is: 3
Vector after removing the last element: 1 2 3 4 
```

**Conclusion:**
We have successfully demonstrated the use of the STL `vector` container, including adding, accessing, and removing elements. This shows the power and convenience of using STL containers for managing collections of data.

**Question 2:** Write C++ code for STL using queue. Explain stack container adaptor with an example.

**Aim:** To write a C++ program that demonstrates the use of the STL `queue` and `stack` container adaptors.

**Objective:**
*   To learn how to use the `queue` and `stack` container adaptors.
*   To understand the difference between a queue (FIFO) and a stack (LIFO).

**Theory:**
*   **Queue:** A container adaptor that provides a First-In, First-Out (FIFO) data structure. Elements are inserted at the back (`push`) and removed from the front (`pop`).
*   **Stack:** A container adaptor that provides a Last-In, First-Out (LIFO) data structure. Elements are inserted and removed from the same end, called the top.

**Code (Queue):**
```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> q;

    // Add elements to the queue
    for (int i = 1; i <= 5; i++) {
        q.push(i);
    }

    // Display the contents of the queue
    std::cout << "Queue elements: ";
    while (!q.empty()) {
        std::cout << q.front() << " ";
        q.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

**Input/Output (Queue):**
```
Queue elements: 1 2 3 4 5 
```

**Code (Stack):**
```cpp
#include <iostream>
#include <stack>

int main() {
    std::stack<int> s;

    // Add elements to the stack
    for (int i = 1; i <= 5; i++) {
        s.push(i);
    }

    // Display the contents of the stack
    std::cout << "Stack elements: ";
    while (!s.empty()) {
        std::cout << s.top() << " ";
        s.pop();
    }
    std::cout << std::endl;

    return 0;
}
```

**Input/Output (Stack):**
```
Stack elements: 5 4 3 2 1 
```

**Conclusion:**
We have successfully demonstrated the use of the STL `queue` and `stack` container adaptors. This assignment helps in understanding the FIFO and LIFO data structures and how to implement them using the STL.

### Assignment 7: Exception Handling

**Question:** Write C++ code for exception handling - e.g. Bank account balance below 1000 throw exception.

**Aim:** To write a C++ program that demonstrates exception handling.

**Objective:**
*   To understand the concept of exception handling in C++.
*   To learn how to use `try`, `catch`, and `throw` to handle errors.

**Theory:**
Exception handling is a mechanism in C++ to handle runtime errors. It allows you to transfer control from one part of a program to another. C++ exception handling is built upon three keywords: `try`, `catch`, and `throw`.

*   **`try`:** A `try` block identifies a block of code for which particular exceptions will be activated. It's followed by one or more `catch` blocks.
*   **`throw`:** A program throws an exception when a problem shows up. This is done using a `throw` keyword.
*   **`catch`:** A `catch` block is where you handle the exception. It is placed after the `try` block.

**Code:**
```cpp
#include <iostream>

class BankAccount {
private:
    double balance;

public:
    BankAccount(double bal) : balance(bal) {}

    void withdraw(double amount) {
        if (balance - amount < 1000) {
            throw "Insufficient balance! Minimum balance of 1000 must be maintained.";
        } else {
            balance -= amount;
            std::cout << "Withdrew " << amount << ". New balance: " << balance << std::endl;
        }
    }
};

int main() {
    BankAccount acc(5000);

    try {
        acc.withdraw(3000);
        acc.withdraw(1500);
    } catch (const char* msg) {
        std::cerr << "Error: " << msg << std::endl;
    }

    return 0;
}
```

**Input/Output:**
```
Withdrew 3000. New balance: 2000
Error: Insufficient balance! Minimum balance of 1000 must be maintained.
```

**Conclusion:**
We have successfully implemented exception handling in a C++ program. The program throws an exception when the bank account balance goes below a certain limit, and the exception is caught and handled gracefully. This demonstrates the importance of exception handling in writing robust and reliable programs.