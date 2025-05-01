
# Oracle SQL Commands for Student Table and Queries (Q31–Q40)

## Create Student Table

```sql
CREATE TABLE Student (
    Sid NUMBER PRIMARY KEY,
    Sname VARCHAR2(50),
    DOB DATE,
    State VARCHAR2(50),
    Gender CHAR(1),
    Category VARCHAR2(20),
    Course VARCHAR2(20)
);
```

## Insert Data into Student Table

```sql
INSERT ALL
    INTO Student VALUES (1001, 'Neha', TO_DATE('29-Dec-2002','DD-Mon-YYYY'), 'Telangana', 'F', 'Gen', 'Comp')
    INTO Student VALUES (1002, 'Arun', TO_DATE('10-Jan-2002','DD-Mon-YYYY'), 'Telangana', 'M', 'OBC', 'Honors')
    INTO Student VALUES (1003, 'Payal', TO_DATE('15-Aug-2001','DD-Mon-YYYY'), 'Maharashtra', 'F', 'Gen', 'Appl')
    INTO Student VALUES (1004, 'Amrita', TO_DATE('20-Apr-2002','DD-Mon-YYYY'), 'Karnataka', 'F', 'OBC', 'Honors')
    INTO Student VALUES (1005, 'Pavan', TO_DATE('29-May-2003','DD-Mon-YYYY'), 'AndhraPradesh', 'M', 'ExServicemen', 'Comp')
    INTO Student VALUES (1006, 'Anchal', TO_DATE('01-May-2003','DD-Mon-YYYY'), 'Gujarat', 'F', 'OBC', 'Comp')
    INTO Student VALUES (1007, 'Ramya', TO_DATE('13-Jan-2002','DD-Mon-YYYY'), 'Telangana', 'F', 'Gen', 'Appl')
    INTO Student VALUES (1008, 'Rakesh', TO_DATE('22-Dec-2001','DD-Mon-YYYY'), 'AndhraPradesh', 'M', 'Sports', 'Comp')
SELECT * FROM dual;
```

## Q31. Students not from Telangana or AndhraPradesh

```sql
SELECT * FROM Student 
WHERE State NOT IN ('Telangana', 'AndhraPradesh');
```

## Q32. View for Sid and Sname of Telangana students

```sql
CREATE VIEW Telangana_Students AS
SELECT Sid, Sname FROM Student
WHERE State = 'Telangana';
```

## Q33. Create Index on column Sname

```sql
CREATE INDEX idx_sname ON Student(Sname);
```

## Q34. Female students in Comp course and OBC category

```sql
SELECT * FROM Student
WHERE Gender = 'F' AND Course = 'Comp' AND Category = 'OBC';
```

## Q35. Student ids, names, and their percentage

```sql
-- This assumes a 'percentage' column exists
SELECT Sid, Sname, percentage FROM Student;
```

## Q36. Students ordered by name within each course

```sql
SELECT * FROM Student
ORDER BY Course, Sname ASC;
```

## Q37. Delete students in Comp course born after 2002

```sql
DELETE FROM Student
WHERE Course = 'Comp' AND EXTRACT(YEAR FROM DOB) > 2002;
```

## Q38. Add columns Contactno and Email

```sql
ALTER TABLE Student ADD (Contactno VARCHAR2(15), Email VARCHAR2(100));
```

## Q39. Display names with Mr./Ms. prefix based on gender

```sql
SELECT 
    Sid,
    CASE 
        WHEN Gender = 'M' THEN 'Mr. ' || Sname 
        WHEN Gender = 'F' THEN 'Ms. ' || Sname 
    END AS Prefixed_Name
FROM Student;
```

## Q40. Students with name length = 5 characters

```sql
SELECT * FROM Student
WHERE LENGTH(Sname) = 5;
```
