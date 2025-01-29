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
