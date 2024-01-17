# SQL-Challenge

**Background**
This repository discusses a research project on the employee database at Pewlett Hackard Corporation from the 1980s and 1990s. All that remains of the database of employees from that period is in six CSV files.

On this project, a table was created that holds employees data in the CSVs, import the CSVs into a SQL database, and the data exploration was conducted to answering the research questions, and discussed in the following parts:

**1. Data Modeling**
To model the employee data a basic data modeling technique called Entity-Relationship Diagrams (ERD) was used. By using this technique six employee database entities or tables are identified, these entities are employees, departments, salaries, titles, department managers, and department employees. The attribute or the data type of the entities also presented. At last, the ER diagram was drawn to visualize the relationships between entities/objects (primary key or foreign keys in a database). 

**2. Data Engineering**
By using the available information a table schema for each of the six CSV files was created, and the data types, primary keys, foreign keys, and constraints also developed. The order of the table is based on the primary, and foreign arrangements.

Note to import each CSV file into the corresponding SQL table the order strictly should be followed to avoid errors.

**3. Data Analysis**
After completing the importing process a Postgresql analysiss was perfomed and you can find the full query in this file Employees_db_Query.sql

The analysis query performed, and cascaded in the following formats:

**The query to list the following details of each employee: employee number, last name, first name, sex, and salary**
FROM employees
JOIN salaries
ON employees.emp_no = salaries.emp_no;

**The query to list first name, last name, and hire date for employees who were hired in 1986.**
SELECT first_name, last_name, hire_date 
FROM employees
WHERE hire_date BETWEEN '1986-01-01' AND '1987-01-01';

**The query list the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name.**
SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name
FROM departments
JOIN dept_manager
ON departments.dept_no = dept_manager.dept_no
JOIN employees
ON dept_manager.emp_no = employees.emp_no;

**The query to list the department of each employee with the following information: employee number, last name, first name, and department name.**
SELECT dept_emp.dept_no, dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no

**The query to list first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B."**
SELECT first_name, last_name,sex
FROM employees
WHERE first_name = 'Hercules'
AND last_name LIKE 'B%'

**The query to list all employees in the Sales department, including their employee number, last name, first name, and department name.**
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE dept_name = 'Sales'

**The query to list all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.**
SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM dept_emp
JOIN employees
ON dept_emp.emp_no = employees.emp_no
JOIN departments
ON dept_emp.dept_no = departments.dept_no
WHERE dept_name = 'Sales'
OR dept_name = 'Development'

**In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.**
SELECT last_name,
COUNT(last_name) AS "Frequency"
FROM employees
GROUP BY last_name
ORDER BY
COUNT(last_name) DESC
