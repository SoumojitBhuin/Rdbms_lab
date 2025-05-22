```sql 

CREATE TABLE account (
    account_id NUMBER PRIMARY KEY,
    Name VARCHAR2(100) NOT NULL,
    balance NUMBER(15, 2) NOT NULL
);



INSERT INTO account (account_id, Name, balance) VALUES (101, 'Alice', 10000);
INSERT INTO account (account_id, Name, balance) VALUES (102, 'Bob', 3500);
INSERT INTO account (account_id, Name, balance) VALUES (103, 'Charlie', 2500);
INSERT INTO account (account_id, Name, balance) VALUES (104, 'Diana', 1800);
INSERT INTO account (account_id, Name, balance) VALUES (105, 'Ethan', 500);



CREATE OR REPLACE PROCEDURE debit_account(p_account_id IN NUMBER) AS
    v_balance      account.balance%TYPE;
    v_debit_amount CONSTANT NUMBER := 2000;
    v_min_balance  CONSTANT NUMBER := 500;
BEGIN
    -- Get current balance
    SELECT balance INTO v_balance
    FROM account
    WHERE account_id = p_account_id;

    -- Check if enough balance remains
    IF (v_balance - v_debit_amount) >= v_min_balance THEN
        UPDATE account
        SET balance = balance - v_debit_amount
        WHERE account_id = p_account_id;

        COMMIT;
        DBMS_OUTPUT.PUT_LINE('Rs 2000 debited successfully. New balance is ' || (v_balance - v_debit_amount));
    ELSE
        DBMS_OUTPUT.PUT_LINE('Insufficient balance. Minimum Rs 500 must remain.');
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Account number ' || p_account_id || ' not found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected error: ' || SQLERRM);
END;
/

-- Step 4: Accept input and call the procedure
ACCEPT acc_no NUMBER PROMPT 'Enter Account Number: '

BEGIN
    debit_account(&acc_no);
END;
/
```
