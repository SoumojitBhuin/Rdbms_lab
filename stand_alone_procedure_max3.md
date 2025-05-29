```sql
CREATE OR REPLACE PROCEDURE max_num (a NUMBER, b NUMBER, c NUMBER)
AS
    max_value NUMBER;
BEGIN
    max_value := GREATEST(a,b,c);
    DBMS_OUTPUT.PUT_LINE(max_value);
END max_num;

```