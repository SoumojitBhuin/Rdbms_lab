```sql
DECLARE
    n NUMBER := 100; -- Upper limit for prime numbers
    i NUMBER;
    j NUMBER;
    is_prime BOOLEAN;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Prime numbers up to ' || n || ':');

    FOR i IN 2..n LOOP
        is_prime := TRUE;

        FOR j IN 2..TRUNC(SQRT(i)) LOOP
            IF MOD(i, j) = 0 THEN
                is_prime := FALSE;
                EXIT;
            END IF;
        END LOOP;

        IF is_prime THEN
            DBMS_OUTPUT.PUT_LINE(i);
        END IF;
    END LOOP;
END;
/
```