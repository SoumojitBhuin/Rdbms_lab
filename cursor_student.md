### Step 1: Table Structure
```sql
CREATE TABLE student (
    rollno     NUMBER PRIMARY KEY,
    name       VARCHAR2(50),
    s1         NUMBER,
    s2         NUMBER,
    s3         NUMBER,
    s4         NUMBER,
    total      NUMBER,
    percentage NUMBER
);
```
###  Step 2: Insert Sample Data
```sql
INSERT INTO student (rollno, name, s1, s2, s3, s4) VALUES (1, 'Alice', 85, 90, 80, 95);
INSERT INTO student (rollno, name, s1, s2, s3, s4) VALUES (2, 'Bob', 70, 75, 65, 60);
INSERT INTO student (rollno, name, s1, s2, s3, s4) VALUES (3, 'Charlie', 88, 92, 85, 90);
COMMIT;
```
###  Step 3: Cursor Program to Calculate Total and Percentage
```sql
DECLARE
    -- Cursor to fetch student marks
    CURSOR student_cur IS
        SELECT rollno, s1, s2, s3, s4
        FROM student;

    -- Variables to store individual row values
    v_rollno     student.rollno%TYPE;
    v_s1         student.s1%TYPE;
    v_s2         student.s2%TYPE;
    v_s3         student.s3%TYPE;
    v_s4         student.s4%TYPE;
    v_total      NUMBER;
    v_percentage NUMBER;
BEGIN
    OPEN student_cur;
    LOOP
        FETCH student_cur INTO v_rollno, v_s1, v_s2, v_s3, v_s4;
        EXIT WHEN student_cur%NOTFOUND;

        -- Calculate total and percentage
        v_total := v_s1 + v_s2 + v_s3 + v_s4;
        v_percentage := (v_total / 400) * 100; -- assuming each subject is out of 100

        -- Update the student record
        UPDATE student
        SET total = v_total,
            percentage = v_percentage
        WHERE rollno = v_rollno;
    END LOOP;
    CLOSE student_cur;

    COMMIT;
    DBMS_OUTPUT.PUT_LINE('Total and Percentage calculated for all students.');
END;
/
```
###  Step 4: View Results
```sql
SELECT * FROM student;

```
