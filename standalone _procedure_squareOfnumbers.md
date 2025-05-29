```sql
CREATE OR REPLACE PROCEDURE sq_num (b NUMBER)
AS
    c NUMBER;
BEGIN
    c := b*b;
    DBMS_OUTPUT.PUT_LINE ('Square of ' || b || ' is ' || c);
END sq_num;
```