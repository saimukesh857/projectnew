# projectnew
// Java Concepts Demonstration
// Covers: Classes, Objects, Arrays, Encapsulation, Inheritance, Polymorphism,
// Abstract class, Constructor, Final, Static, GC(), Collections, Exception Handling.

import java.util.*;

// 1️⃣ Abstract Class
abstract class Person {
    private String name;   // encapsulation
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters (Encapsulation)
    public String getName() { return name; }
    public int getAge() { return age; }

    // Abstract method (must be implemented by child)
    public abstract void displayInfo();
}

// 2️⃣ Subclass + Inheritance + Polymorphism
class Employee extends Person {
    private double salary;
    private final String empCode;   // Final variable
    private static int empCount = 0; // Static variable (shared)

    // Constructor
    public Employee(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
        empCount++;
        this.empCode = "EMP" + empCount;
    }

    // Method overriding (Polymorphism)
    @Override
    public void displayInfo() {
        System.out.println("Employee Code: " + empCode +
                ", Name: " + getName() +
                ", Age: " + getAge() +
                ", Salary: " + salary);
    }

    public static int getEmpCount() {
        return empCount;
    }
}

// 3️⃣ Exception Handling
class InvalidSalaryException extends Exception {
    public InvalidSalaryException(String message) {
        super(message);
    }
}

// 4️⃣ Main Class
public class MainConceptDemo {

    public static void main(String[] args) {
        try {
            // Creating array of objects (Object Array)
            Employee[] employees = new Employee[3];
            employees[0] = new Employee("Alice", 28, 50000);
            employees[1] = new Employee("Bob", 30, 60000);
            employees[2] = new Employee("Charlie", 35, 75000);

            // Display all employees
            System.out.println("=== Employee Details ===");
            for (Employee e : employees) {
                e.displayInfo(); // polymorphism in action
            }

            // Using Collections Framework (ArrayList)
            List<Employee> empList = new ArrayList<>(Arrays.asList(employees));

            System.out.println("\n=== Using Collections Framework ===");
            empList.forEach(Employee::displayInfo);

            // Sorting collection using Comparator (by salary descending)
            empList.sort(Comparator.comparing(Employee::getAge).reversed());
            System.out.println("\n=== Sorted by Age (Descending) ===");
            empList.forEach(Employee::displayInfo);

            // Exception Handling Example
            double testSalary = -5000;
            if (testSalary < 0) {
                throw new InvalidSalaryException("Salary cannot be negative!");
            }

        } catch (InvalidSalaryException e) {
            System.out.println("❌ Exception Caught: " + e.getMessage());
        } finally {
            System.out.println("\nFinal block executed — cleaning up resources.");
        }

        // Demonstrate static and final
        System.out.println("\nTotal Employees Created: " + Employee.getEmpCount());

        // Request Garbage Collection (just a hint to JVM)
        System.gc();
        System.out.println("Garbage Collector invoked (System.gc()).");

        System.out.println("\n✅ Program Executed Successfully!");
    }
}
