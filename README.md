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
