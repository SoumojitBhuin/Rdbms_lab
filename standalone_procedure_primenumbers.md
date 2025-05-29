```sql
CREATE OR REPLACE PROCEDURE primenumber_DISP(a NUMBER, b NUMBER)
AS
    i NUMBER;
    j NUMBER;
    is_prime BOOLEAN;
BEGIN
    FOR i IN a..b LOOP
        is_prime := TRUE;

        FOR j IN 2..TRUNC(SQRT(i)) LOOP
            IF MOD(i,j) = 0 THEN
                is_prime := FALSE;
            END IF;
        END LOOP;

        IF is_prime THEN
            DBMS_OUTPUT.PUT_LINE(i);
        END IF;
    END LOOP;
END primenumber_DISP;
```