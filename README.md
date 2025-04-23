# postgreSQL basics
Quick reference when it gets rusty.

### BASIC COMMANDS
| SQL | Explaination |
|------------|-------|
\l           | List all db |
\c my_db     | Connect to a db |
\dt          | List all tables |
\d my_table  | Describe a table |
\i file.sql  | Run SQL file |

### DATA TYPES
- INTEGER
- SERIAL (Auto-increment)
- TEXT
- VARCHAR(n) (TEXT with max n characters)
- BOOLEAN
- DATE (YYYY-MM-DD)
- TIMESTAMP
- NUMERIC(p,s) (p=total digits, s=total decimal point)

### CRUD
- INSERT INTO employees (name, age) VALUES ('Abu', 23);
- SELECT location, AVG(salary) AS avg_salary FROM employees WHERE employment_year <= 2 GROUP BY location ;
- UPDATE employees SET location = 'Johor' WHERE id = 4 ;
- DELETE FROM employees WHERE id = 2 ;

### TABLE OPERATIONS
CREATE TABLE employees { 
id SERIAL PRIMARY KEY,
name TEXT NOT NULL,
age INTEGER,
location TEXT,
salary NUMERIC(10,2)
};
ALTER TABLE employees ADD COLUMN email TEXT UNIQUE;
DROP TABLE employees;

### JOINS
- INNER JOIN (no nulls on either side)
SELECT e.name, d.name
FROM employees e
JOIN departments d
ON e.dept_id = d.id;
- LEFT JOIN (LEFT is prioritised - nulls may exist on RHS) 
- RIGHT JOIN (vice versa)
- FULL JOIN (nulls may exist on BOTH sides)

### FILTER, SORT, GROUP, AGGREGATE
SELECT name, salary FROM employees WHERE salary > 2500 ORDER BY salary DESC ;
SELECT location, COUNT(*) AS total_employees_by_state
FROM employees
GROUP BY location
HAVING COUNT(*) > 2
ORDER BY total_employees_by_state ASC;

### SUBQUERY
SELECT name FROM employees
WHERE dept_id = (SELECT id FROM departments WHERE dept_name = 'IT');

### FUNCTIONS & EXPRESSIONS
- concat string
SELECT first_name || ' ' || last_name AS full_name FROM employees;
- case
SELECT name,
CASE
  WHEN location = 'Sabah' THEN 'Sarawak'
  ELSE 'Other'
END
FROM employees;

