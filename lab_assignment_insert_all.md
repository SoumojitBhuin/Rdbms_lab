
# LAB Assignment (Home Assignment) - SQL Solutions

## Create Tables

```sql
CREATE TABLE Department (
    DeptId VARCHAR2(2) PRIMARY KEY,
    Dname VARCHAR2(20) NOT NULL
);

CREATE TABLE Employee (
    Eid NUMBER PRIMARY KEY,
    Ename VARCHAR2(20),
    DeptId VARCHAR2(2),
    Designation VARCHAR2(20),
    Salary NUMBER CHECK (Salary > 10000),
    DOJ DATE,
    FOREIGN KEY (DeptId) REFERENCES Department(DeptId)
);
```

## Insert Values

```sql
-- Insert into Department using INSERT ALL
INSERT ALL
    INTO Department (DeptId, Dname) VALUES ('D1', 'Sales')
    INTO Department (DeptId, Dname) VALUES ('D2', 'Marketing')
    INTO Department (DeptId, Dname) VALUES ('D3', 'Finance')
SELECT * FROM dual;

-- Insert into Employee using INSERT ALL
INSERT ALL
    INTO Employee VALUES (101, 'Sudha', 'D2', 'Clerk', 20000, TO_DATE('01-Apr-2010', 'DD-Mon-YYYY'))
    INTO Employee VALUES (102, 'David', 'D1', 'Manager', 50000, TO_DATE('18-Feb-2018', 'DD-Mon-YYYY'))
    INTO Employee VALUES (103, 'Preethi', 'D3', 'Clerk', 35000, TO_DATE('13-Jun-2011', 'DD-Mon-YYYY'))
    INTO Employee VALUES (104, 'Kiran', 'D1', 'Salesman', 20000, TO_DATE('07-Mar-2014', 'DD-Mon-YYYY'))
    INTO Employee VALUES (105, 'Meenal', 'D2', 'Clerk', 50000, TO_DATE('09-Dec-2011', 'DD-Mon-YYYY'))
    INTO Employee VALUES (106, 'Sunitha', 'D3', 'Manager', 60000, TO_DATE('25-Sep-2018', 'DD-Mon-YYYY'))
    INTO Employee VALUES (107, 'Akhil', 'D3', 'Clerk', 25000, TO_DATE('14-Feb-2016', 'DD-Mon-YYYY'))
    INTO Employee VALUES (108, 'Sushma', 'D2', 'Manager', 45000, TO_DATE('31-Jan-2012', 'DD-Mon-YYYY'))
SELECT * FROM dual;
```

---

## Query Solutions

### 21. Employees earning more than average salary

```sql
SELECT * FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

### 22. Display Eid, Ename, and Dname

```sql
SELECT E.Eid, E.Ename, D.Dname
FROM Employee E
JOIN Department D ON E.DeptId = D.DeptId;
```

### 23. Sort employees by salary (descending)

```sql
SELECT * FROM Employee
ORDER BY Salary DESC;
```

### 24. List all job designations without repetitions

```sql
SELECT DISTINCT Designation FROM Employee;
```

### 25. Employee details department-wise and ascending by salary

```sql
SELECT * FROM Employee
ORDER BY DeptId, Salary ASC;
```

### 26. Display all clerks in DeptId D2

```sql
SELECT * FROM Employee
WHERE Designation = 'Clerk' AND DeptId = 'D2';
```

### 27. Employees who joined in 2011

```sql
SELECT * FROM Employee
WHERE EXTRACT(YEAR FROM DOJ) = 2011;
```

### 28. Employees who joined in February

```sql
SELECT * FROM Employee
WHERE EXTRACT(MONTH FROM DOJ) = 2;
```

### 29. Employees with salary between 30000 and 45000

```sql
SELECT * FROM Employee
WHERE Salary BETWEEN 30000 AND 45000;
```

### 30. Employees with work experience till current date

```sql
SELECT *, FLOOR(MONTHS_BETWEEN(SYSDATE, DOJ)/12) AS Years_of_Experience
FROM Employee;
```

---

Department of Information Technology, NEHU
