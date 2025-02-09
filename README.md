# MongoDB_DBA
CREATE DATABASE ORG1234;
SHOW DATABASES;
USE ORG1234;

CREATE TABLE Worker (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT(15),
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account');
        
select * from worker
where department='Admin' order by department;

select department, count(department) as total_employees from worker
where department = 'HR' or department = 'account' group by department;

select department, count(department) as total_employees from worker
group by department
order by total_employees desc;

SELECT DEPARTMENT, COUNT(*) AS DepartmentCount
FROM Worker
GROUP BY DEPARTMENT
HAVING COUNT(*) = (SELECT MAX(DepartmentCount) FROM (SELECT DEPARTMENT, COUNT(*) AS DepartmentCount FROM Worker GROUP BY DEPARTMENT) AS Counts);

SELECT DEPARTMENT, COUNT(*) AS DepartmentCount
FROM Worker
GROUP BY DEPARTMENT
HAVING COUNT(*) = (SELECT MIN(DepartmentCount) FROM (SELECT DEPARTMENT, COUNT(*) AS DepartmentCount FROM Worker GROUP BY DEPARTMENT) AS Counts);

SELECT department, COUNT(*) AS departmentCount
FROM worker
GROUP BY department
HAVING COUNT(*) = (
    SELECT MAX(departmentCount)
    FROM (
        SELECT COUNT(*) AS departmentCount
        FROM worker
        GROUP BY department
    ) AS subquery
);

insert into worker value (008, 'kumar', 'Satish', 75000, '14-01-20 09.00.00', 'Account');

USE ORG1234;

CREATE TABLE WorkerWithCity (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT(15),
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25),
    CITY varchar(255) DEFAULT 'India'
);

INSERT INTO WorkerWithCity 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT, CITY) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR', 'GOA'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin', 'Pondicherry'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR',''),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin',''),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin',''),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account',''),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account', 'Jammu');
        
SELECT * FROM WorkerWithCity;

select * from workerWithCity
where city like '_o_';

create view Salary_more_than_3lac as
select * from workerWithCity
where salary > 300000
order by salary desc;

select first_name from salary_more_than_3lac;

create or replace view Salary_more_than_3lac as
select first_name from workerWithCity
where salary > 300000
order by salary desc;

select * from salary_more_than_3lac;

drop view salary_more_than_3lac;

CREATE DATABASE ORG1235;
SHOW DATABASES;
USE ORG1235;

CREATE TABLE Worker (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT(15),
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'),
		(008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');

CREATE TABLE Bonus (
	WORKER_REF_ID INT,
	BONUS_AMOUNT INT(10),
	BONUS_DATE DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);

INSERT INTO Bonus 
	(WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
		(001, 5000, '16-02-20'),
		(002, 3000, '16-06-11'),
		(003, 4000, '16-02-20'),
		(001, 4500, '16-02-20'),
        (002, 3500, '16-06-11');
        
select * from worker
where first_name not in ('vipul', 'satish');

select * from worker
where first_name like '%a';

select * from worker
where first_name like '_____h';

select department, count(department) as total_employees from worker
group by department
order by total_employees desc;

SELECT * FROM Worker
UNION ALL
SELECT * FROM Worker
