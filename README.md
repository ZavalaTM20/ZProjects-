#Random SQL Codes during my First College Sesmester of Sophmore Year 

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Position VARCHAR(50),
    Department VARCHAR(50),
    Salary DECIMAL(10, 2),
    HireDate DATE
);

-- Insert sample data
INSERT INTO Employees (EmployeeID, FirstName, LastName, Position, Department, Salary, HireDate)
VALUES
(1, 'John', 'Doe', 'Software Engineer', 'IT', 80000.00, '2021-05-15'),
(2, 'Jane', 'Smith', 'HR Manager', 'HR', 75000.00, '2020-03-22'),
(3, 'Alice', 'Johnson', 'Product Manager', 'Product', 95000.00, '2019-07-10');

-- Query to find all employees in the IT department
SELECT * FROM Employees WHERE Department = 'IT';

CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Major VARCHAR(100)
);

-- Create Courses Table
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(255),
    Credits INT
);

-- Create Enrollments Table (Many-to-many relationship)
CREATE TABLE Enrollments (
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

#2 This is my course work from class 
-- Insert sample data into Students
INSERT INTO Students (StudentID, FirstName, LastName, Major)
VALUES
(1, 'John', 'Doe', 'Computer Science'),
(2, 'Jane', 'Smith', 'Biology');

-- Insert sample data into Courses
INSERT INTO Courses (CourseID, CourseName, Credits)
VALUES
(1, 'Introduction to Programming', 3),
(2, 'Biology 101', 4);

-- Insert sample data into Enrollments
INSERT INTO Enrollments (StudentID, CourseID, EnrollmentDate)
VALUES
(1, 1, '2025-01-10'),
(2, 2, '2025-01-12');

-- Query to list all courses a student is enrolled in
SELECT Courses.CourseName, Enrollments.EnrollmentDate
FROM Enrollments
JOIN Courses ON Enrollments.CourseID = Courses.CourseID
WHERE Enrollments.StudentID = 1;



#Python Student Mangment Coding from In-Class and Own Time



conn = sqlite3.connect('student_management.db')
cursor = conn.cursor()

cursor.execute('''
    CREATE TABLE IF NOT EXISTS Students (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        age INTEGER,
        grade TEXT
    )
''')


def add_student():
    name = input("Enter student's name: ")
    age = int(input("Enter student's age: "))
    grade = input("Enter student's grade: ")
    
    cursor.execute('''
        INSERT INTO Students (name, age, grade) 
        VALUES (?, ?, ?)
    ''', (name, age, grade))
    
    conn.commit()
    print(f"Student {name} added successfully!")

def view_students():
    cursor.execute("SELECT * FROM Students")
    students = cursor.fetchall()
    
    if students:
        print("\nList of Students:")
        for student in students:
            print(f"ID: {student[0]}, Name: {student[1]}, Age: {student[2]}, Grade: {student[3]}")
    else:
        print("No students found.")

def update_student():
    student_id = int(input("Enter the student's ID to update: "))
    new_name = input("Enter the new name (leave blank to keep the current name): ")
    new_age = input("Enter the new age (leave blank to keep the current age): ")
    new_grade = input("Enter the new grade (leave blank to keep the current grade): ")

    # Fetch current data
    cursor.execute("SELECT * FROM Students WHERE id = ?", (student_id,))
    student = cursor.fetchone()
    
    if student:
        # Update values only if the new data is provided
        name = new_name if new_name else student[1]
        age = int(new_age) if new_age else student[2]
        grade = new_grade if new_grade else student[3]
        
        cursor.execute('''
            UPDATE Students
            SET name = ?, age = ?, grade = ?
            WHERE id = ?
        ''', (name, age, grade, student_id))
        
        conn.commit()
        print(f"Student ID {student_id} updated successfully!")
    else:
        print(f"No student found with ID {student_id}.")

def delete_student():
    student_id = int(input("Enter the student's ID to delete: "))
    cursor.execute("SELECT * FROM Students WHERE id = ?", (student_id,))
    student = cursor.fetchone()

    if student:
        cursor.execute("DELETE FROM Students WHERE id = ?", (student_id,))
        conn.commit()
        print(f"Student ID {student_id} deleted successfully!")
    else:
        print(f"No student found with ID {student_id}.")

def main():
    while True:
        print("\n--- Student Management System ---")
        print("1. Add Student")
        print("2. View All Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. Exit")
        
        choice = input("Enter your choice (1-5): ")
        
        if choice == '1':
            add_student()
        elif choice == '2':
            view_students()
        elif choice == '3':
            update_student()
        elif choice == '4':
            delete_student()
        elif choice == '5':
            print("Exiting the system.")
            break
        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()

conn.close()
