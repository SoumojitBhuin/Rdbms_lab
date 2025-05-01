
# LAB Assignment (Home Assignment) - Student Table SQL Solutions

## Create Student Table

```sql
CREATE TABLE Student (
    Sid NUMBER PRIMARY KEY,
    Sname VARCHAR2(20),
    DOB DATE,
    State VARCHAR2(20),
    Gender CHAR(1),
    Category VARCHAR2(20),
    Course VARCHAR2(20)
);
```

## Insert Values Using INSERT ALL

```sql
INSERT ALL
    INTO Student VALUES (1001, 'Neha', TO_DATE('29-Dec-2002', 'DD-Mon-YYYY'), 'Telangana', 'F', 'Gen', 'Comp')
    INTO Student VALUES (1002, 'Arun', TO_DATE('10-Jan-2002', 'DD-Mon-YYYY'), 'Telangana', 'M', 'OBC', 'Honors')
    INTO Student VALUES (1003, 'Payal', TO_DATE('15-Aug-2001', 'DD-Mon-YYYY'), 'Maharashtra', 'F', 'Gen', 'Appl')
    INTO Student VALUES (1004, 'Amrita', TO_DATE('20-Apr-2002', 'DD-Mon-YYYY'), 'Karnataka', 'F', 'OBC', 'Honors')
    INTO Student VALUES (1005, 'Pavan', TO_DATE('29-May-2003', 'DD-Mon-YYYY'), 'AndhraPradesh', 'M', 'ExServicemen', 'Comp')
    INTO Student VALUES (1006, 'Anchal', TO_DATE('01-May-2003', 'DD-Mon-YYYY'), 'Gujarat', 'F', 'OBC', 'Comp')
    INTO Student VALUES (1007, 'Ramya', TO_DATE('13-Jan-2002', 'DD-Mon-YYYY'), 'Telangana', 'F', 'Gen', 'Appl')
    INTO Student VALUES (1008, 'Rakesh', TO_DATE('22-Dec-2001', 'DD-Mon-YYYY'), 'AndhraPradesh', 'M', 'Sports', 'Comp')
SELECT * FROM dual;
```

---

## Queries

### 31. Students not from Telangana or AndhraPradesh

```sql
SELECT * FROM Student
WHERE State NOT IN ('Telangana', 'AndhraPradesh');
```

### 32. View for students from Telangana (Sid, Sname)

```sql
CREATE VIEW Telangana_Students AS
SELECT Sid, Sname FROM Student
WHERE State = 'Telangana';
```

### 33. Create index on Sname

```sql
CREATE INDEX idx_sname ON Student(Sname);
```

### 34. Female students in Comp course and OBC category

```sql
SELECT * FROM Student
WHERE Gender = 'F' AND Course = 'Comp' AND Category = 'OBC';
```

### 35. Display Sid, Sname, and present age

```sql
SELECT Sid, Sname, FLOOR(MONTHS_BETWEEN(SYSDATE, DOB)/12) AS Age
FROM Student;
```

### 36. Students in ascending order of names for each course

```sql
SELECT * FROM Student
ORDER BY Course, Sname ASC;
```

### 37. Delete students in Comp course born after 2002

```sql
DELETE FROM Student
WHERE Course = 'Comp' AND DOB > TO_DATE('31-Dec-2002', 'DD-Mon-YYYY');
```

### 38. Add Contactno and Email columns

```sql
ALTER TABLE Student ADD (Contactno VARCHAR2(15), Email VARCHAR2(50));
```

### 39. Display student names prefixed with Mr./Ms.

```sql
SELECT Sid,
       CASE 
           WHEN Gender = 'M' THEN 'Mr. ' || Sname
           WHEN Gender = 'F' THEN 'Ms. ' || Sname
       END AS Prefixed_Name
FROM Student;
```

### 40. Students whose names have exactly 5 characters

```sql
SELECT * FROM Student
WHERE LENGTH(Sname) = 5;
```

---

Department of Information Technology, NEHU
