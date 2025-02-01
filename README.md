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


# Connect to SQLite database (or create it if it doesn't exist)
conn = sqlite3.connect('student_management.db')
cursor = conn.cursor()

# Create the Students table
cursor.execute('''
    CREATE TABLE IF NOT EXISTS Students (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        age INTEGER,
        grade TEXT
    )
''')

# Function to add a student
def add_student():
    name = input("Enter student's name: ")
    age = int(input("Enter student's age: "))
    grade = input("Enter student's grade: ")
    

# Function to view all students
def view_students():
    cursor.execute("SELECT * FROM Students")
    students = cursor.fetchall()
    

# Function to update a student's information
def update_student():
    student_id = int(input("Enter the student's ID to update: "))
    new_name = input("Enter the new name (leave blank to keep the current name): ")
    new_age = input("Enter the new age (leave blank to keep the current age): ")
    new_grade = input("Enter the new grade (leave blank to keep the current grade): ")



# Function to delete a student
def delete_student():
    student_id = int(input("Enter the student's ID to delete: "))
    cursor.execute("SELECT * FROM Students WHERE id = ?", (student_id,))
    student = cursor.fetchone()



# Main menu
def main():
    while True:
        print("\n--- Student Management System ---")
        print("1. Add Student")
        print("2. View All Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. Exit")
        
        
# Run the program
if __name__ == "__main__":
    main()

# Close the connection when done
conn.close()
