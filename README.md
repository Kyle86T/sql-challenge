# sql-challenge
# Created tables, and answered the questions based on the table data.
-- drop table departments;
create table departments (
  	dept_no VARCHAR(30) NOT NULL primary key,
  	dept_name VARCHAR(30) NOT NULL
);
select * from departments
-- drop table dept_emp;
create table dept_emp (
  	emp_no int,
  	dept_no VARCHAR(30) NOT NULL
);
select * from dept_emp
-- drop table dept_manager;
create table dept_manager (
  	dept_no VARCHAR(30) NOT NULL,
	emp_no int	
);
select * from dept_manager
-- drop table employees;
create table employees (
	emp_no int primary key,
	emp_title_id varchar(30),
	birth_date varchar(30),
	first_name varchar(30),
	last_name varchar(50),
	sex varchar(20),
	hire_date date
);
select * from employees
-- drop table salaries;
create table salaries (
	emp_no int,
	salary int
);
select * from salaries
-- drop table titles;
create table titles (
	title_id varchar(30),
	title  varchar(30)
);
select * from titles

--Question #1: List the following details of each employee: employee number, last name, first name, sex, and salary
select e.emp_no, last_name, first_name, sex, salary
from employees e
inner join salaries s on s.emp_no = e.emp_no
order by emp_no asc

--Question #2: List first name, last name, and hire date for employees who were hired in 1986
select first_name, last_name, hire_date
from employees
where date_part('year', hire_date) = 1986

--Question #3: List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name
select de.dept_no, e.emp_no, last_name, first_name, emp_title_id--,dm.dept_name
from employees e
inner join dept_emp de on de.emp_no=e.emp_no
where emp_title_id = 'm0001'
order by dept_no asc
-- select *
-- from departments d
-- inner join dept_manager dm on dm.dept_no=d.dept_no
-- inner join employees e on dm.emp_no=e.emp_no

--Question #4: List the department of each employee with the following information: employee number, last name, first name, and department name
select e.emp_no, last_name, first_name, dept_name
from employees e
inner join dept_emp de on de.emp_no=e.emp_no
inner join departments d on d.dept_no=de.dept_no

--Question #5: List first name, last name, and sex for employees whose first name is "Hercules" and last names begin with "B"
select first_name, last_name, sex
from employees
where first_name = 'Hercules' and last_name like('B%')

--Question #6: List all employees in the Sales department, including their employee number, last name, first name, and department name
select e.emp_no, last_name, first_name, dept_name
from employees e
inner join dept_emp de on de.emp_no=e.emp_no
inner join departments d on d.dept_no=de.dept_no
where dept_name =  'Sales'

--Question #7: List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name
select e.emp_no, last_name, first_name, dept_name
from employees e
inner join dept_emp de on de.emp_no=e.emp_no
inner join departments d on d.dept_no=de.dept_no
where dept_name =  'Sales' or dept_name = 'Development'

--Question #8: In descending order, list the frequency count of employee last names, i.e., how many employees share each last name
select last_name, count(last_name)
from employees
-- where last_name ='Markovitch'
group by last_name
order by last_name desc

select *
from employees 
where emp_no =  499942
