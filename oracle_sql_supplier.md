
# Oracle SQL Script for Supplier Table

## 1. Table Creation and Data Insertion

```sql
CREATE TABLE Supplier (
    Sup_No VARCHAR2(10) PRIMARY KEY,
    Sup_Name VARCHAR2(50),
    Item_Supplied VARCHAR2(50),
    Item_Price NUMBER,
    City VARCHAR2(50)
);

INSERT ALL
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S1', 'Suresh', 'Keyboard', 400, 'Hyderabad')
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S2', 'Kiran', 'Processor', 8000, 'Delhi')
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S3', 'Mohan', 'Mouse', 350, 'Delhi')
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S4', 'Ramesh', 'Processor', 9000, 'Bangalore')
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S5', 'Manish', 'Printer', 6000, 'Mumbai')
    INTO Supplier (Sup_No, Sup_Name, Item_Supplied, Item_Price, City) VALUES ('S6', 'Srikanth', 'Processor', 8500, 'Chennai')
SELECT * FROM dual;
```

## 2. Queries

### Query 1: Display supplier numbers and names whose name starts with 'R'
```sql
SELECT Sup_No, Sup_Name 
FROM Supplier 
WHERE Sup_Name LIKE 'R%';
```

### Query 2: Display names of suppliers who supply Processors and whose city is Delhi
```sql
SELECT Sup_Name 
FROM Supplier 
WHERE Item_Supplied = 'Processor' AND City = 'Delhi';
```

### Query 3: Display names of suppliers who supply the same items as Ramesh
```sql
SELECT Sup_Name 
FROM Supplier 
WHERE Item_Supplied = (SELECT Item_Supplied FROM Supplier WHERE Sup_Name = 'Ramesh');
```

### Query 4: Increase the price of Keyboard by 200
```sql
UPDATE Supplier 
SET Item_Price = Item_Price + 200 
WHERE Item_Supplied = 'Keyboard';
```

### Query 5: Display supplier numbers, names, and item prices for suppliers in Delhi in ascending order of item price
```sql
SELECT Sup_No, Sup_Name, Item_Price 
FROM Supplier 
WHERE City = 'Delhi' 
ORDER BY Item_Price ASC;
```

### Query 6: Add a new column called CONTACTNO
```sql
ALTER TABLE Supplier 
ADD CONTACTNO VARCHAR2(15);
```

### Query 7: Delete the record whose item price is the lowest among all items supplied
```sql
DELETE FROM Supplier 
WHERE Item_Price = (SELECT MIN(Item_Price) FROM Supplier);
```

### Query 8: Create a view to display only supplier numbers and names
```sql
CREATE VIEW Supplier_View AS 
SELECT Sup_No, Sup_Name 
FROM Supplier;
```

### Query 9: Display records in descending order of item price for each item supplied
```sql
SELECT * 
FROM Supplier 
ORDER BY Item_Supplied, Item_Price DESC;
```

### Query 10: Display records of suppliers who supply items other than Processor or Keyboard
```sql
SELECT * 
FROM Supplier 
WHERE Item_Supplied NOT IN ('Processor', 'Keyboard');
```
