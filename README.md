✅ SECTION A – MCQ ANSWERS (Verified)

C) String

A) 0

B) super

C) Default constructor

B) Same as class name

C) Same method signature

C) Interfaces

B) One abstract method

C) filter()

B) Transforms data

A) collect(Collectors.toList())

A) Java Database Connectivity

B) Statement

B) executeQuery()

A) next()

B) PreparedStatement

A) ->

C) Inheritance

B) Initialize object

B) java.sql

SECTION-B
1) Employee & Manager (Polymorphism Demonstration)

class Employee {
    int id;
    String name;
    double salary;

    // Constructor
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    // Display method
    void display() {
        System.out.println("Employee ID: " + id);
        System.out.println("Employee Name: " + name);
        System.out.println("Salary: " + salary);
    }
}

class Manager extends Employee {
    double bonus;

    // Constructor
    Manager(int id, String name, double salary, double bonus) {
        super(id, name, salary);
        this.bonus = bonus;
    }

    // Overriding display()
    @Override
    void display() {
        super.display();
        System.out.println("Bonus: " + bonus);
        System.out.println("Total Salary: " + (salary + bonus));
    }
}

public class Main {
    public static void main(String[] args) {

        // Polymorphism
        Employee emp = new Manager(101, "Chandana", 50000, 10000);
        emp.display();
    }
}

2) Lambda & Stream API Program

import java.util.*;
import java.util.stream.*;

public class StreamDemo {
    public static void main(String[] args) {

        List<Integer> numbers = Arrays.asList(
                5, 12, 7, 18, 21, 30, 44, 55, 60, 73,
                84, 91, 100, 2, 16
        );

        // Print even numbers
        System.out.println("Even Numbers:");
        numbers.stream()
                .filter(n -> n % 2 == 0)
                .forEach(System.out::println);

        // Sum using reduce()
        int sum = numbers.stream()
                .reduce(0, Integer::sum);

        System.out.println("Sum of Numbers: " + sum);

        // Sort in descending order
        System.out.println("Descending Order:");
        numbers.stream()
                .sorted(Comparator.reverseOrder())
                .forEach(System.out::println);
    }
}

3) JDBC Program (MySQL)

MySQL Table Creation
CREATE DATABASE school;
USE school;

CREATE TABLE Student (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    marks DOUBLE
);

Java JDBC Program
import java.sql.*;

public class JDBCDemo {

    public static void main(String[] args) {

        String url = "jdbc:mysql://localhost:3306/school";
        String user = "root";
        String password = "root";   // change if needed

        try {
            // Load Driver (optional for newer versions)
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(url, user, password);

            String insertQuery = "INSERT INTO Student (id, name, marks) VALUES (?, ?, ?)";
            PreparedStatement ps = con.prepareStatement(insertQuery);

            // Insert 5 records
            for (int i = 1; i <= 5; i++) {
                ps.setInt(1, i);
                ps.setString(2, "Student" + i);
                ps.setDouble(3, 60 + i);
                ps.executeUpdate();
            }

            System.out.println("Records Inserted Successfully!");

            // Fetch all records
            Statement st = con.createStatement();
            ResultSet rs = st.executeQuery("SELECT * FROM Student");

            System.out.println("\nStudent Records:");
            while (rs.next()) {
                System.out.println(
                        rs.getInt("id") + " " +
                        rs.getString("name") + " " +
                        rs.getDouble("marks")
                );
            }

            // Close resources
            rs.close();
            st.close();
            ps.close();
            con.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
