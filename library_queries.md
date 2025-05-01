
# Oracle SQL Commands for Library Table and Queries (Q41–Q50)

## Create Library Table

```sql
CREATE TABLE Library (
    BookId VARCHAR2(10) PRIMARY KEY,
    BookName VARCHAR2(100) NOT NULL,
    Author VARCHAR2(100),
    DatePurchased DATE,
    Publisher VARCHAR2(100),
    Price NUMBER
);
```

## Insert Data into Library Table

```sql
INSERT ALL
    INTO Library VALUES ('B101', 'Cost Accounting', 'Jain Narang', TO_DATE('11-Feb-13','DD-Mon-YY'), 'Kalyani', 800)
    INTO Library VALUES ('B102', 'Business Statistics', 'OP Aggarwal', TO_DATE('22-Dec-11','DD-Mon-YY'), 'Himalaya', 750)
    INTO Library VALUES ('B103', 'Rdbms', 'C J Date', TO_DATE('02-Mar-15','DD-Mon-YY'), 'TMH', 900)
    INTO Library VALUES ('B104', 'Mgmt Accounting', 'RK Sharma', TO_DATE('19-Apr-16','DD-Mon-YY'), 'Kalyani', 450)
    INTO Library VALUES ('B105', 'Operating Systems', 'Galvin', TO_DATE('25-Nov-13','DD-Mon-YY'), 'PHI', 750)
    INTO Library VALUES ('B106', 'Advanced Accounting', 'SC Gupta', TO_DATE('16-Apr-18','DD-Mon-YY'), 'Himalaya', 600)
SELECT * FROM dual;
```

## Q41. Authors from Himalaya publications

```sql
SELECT DISTINCT Author FROM Library
WHERE Publisher = 'Himalaya';
```

## Q42. Total cost of books purchased, grouped by Publisher

```sql
SELECT Publisher, SUM(Price) AS TotalCost FROM Library
GROUP BY Publisher;
```

## Q43. Total number of books under Kalyani publications

```sql
SELECT COUNT(*) AS KalyaniBookCount FROM Library
WHERE Publisher = 'Kalyani';
```

## Q44. Rename column Publisher to Publications

```sql
ALTER TABLE Library RENAME COLUMN Publisher TO Publications;
```

## Q45. Display books in ascending order of DatePurchased

```sql
SELECT * FROM Library
ORDER BY DatePurchased ASC;
```

## Q46. Create index on BookName and Author

```sql
CREATE INDEX idx_book_author ON Library(BookName, Author);
```

## Q47. Books priced between 500 and 700

```sql
SELECT * FROM Library
WHERE Price BETWEEN 500 AND 700;
```

## Q48. Increase price of all books by 200 for publishers other than Himalaya or Kalyani

```sql
UPDATE Library
SET Price = Price + 200
WHERE Publisher NOT IN ('Himalaya', 'Kalyani');
```

## Q49. Book details where author name contains 'Sharma'

```sql
SELECT * FROM Library
WHERE Author LIKE '%Sharma%';
```

## Q50. View with BookId and BookName for Publisher Himalaya

```sql
CREATE VIEW HimalayaBooks AS
SELECT BookId, BookName FROM Library
WHERE Publisher = 'Himalaya';
```
