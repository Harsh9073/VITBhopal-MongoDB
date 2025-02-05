# SQLPractice
CREATE DATABASE ORG123;
SHOW DATABASES;
USE ORG123;

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
select * from Worker;
select distinct (department) from worker;
select WORKER_ID as emp_code from worker;
SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
SELECT department, worker_id FROM worker
WHERE salary=100000
UNION
SELECT department, worker_id FROM worker
WHERE salary=200000
ORDER BY worker_id;
SELECT DEPARTMENT, WORKER_ID 
FROM Worker 
WHERE DEPARTMENT = 'HR' 

UNION 

SELECT DEPARTMENT, WORKER_ID 
FROM Worker 
WHERE DEPARTMENT ='Account';

SELECT worker_id, first_name,department,
CASE
    WHEN salary > 300000 THEN 'Rich people'
    WHEN salary <=300000 && salary >=100000 THEN 'Middle stage'
    ELSE 'Poor people'
END 
AS People_stage_wise
FROM worker;

SELECT DISTINCT DEPARTMENT, 
       (SELECT COUNT(*) FROM Worker w WHERE w.DEPARTMENT = Worker.DEPARTMENT) AS TOTAL_EMPLOYEES
FROM Worker
UNION
SELECT 'Total' AS DEPARTMENT, COUNT(*) AS TOTAL_EMPLOYEES FROM Worker;



select * from worker where department='Admin' order by department desc;

(SELECT DEPARTMENT, COUNT(*) AS TOTAL_EMPLOYEES
 FROM Worker
 GROUP BY DEPARTMENT
 ORDER BY TOTAL_EMPLOYEES DESC
 LIMIT 1)
 
UNION

(SELECT DEPARTMENT, COUNT(*) AS TOTAL_EMPLOYEES
 FROM Worker
 GROUP BY DEPARTMENT
 ORDER BY TOTAL_EMPLOYEES ASC LIMIT 1);
 
SELECT DEPARTMENT, COUNT(DEPARTMENT) AS TOTAL_EMPLOYEES  FROM Worker
GROUP BY DEPARTMENT
ORDER BY TOTAL_EMPLOYEES DESC 
LIMIT 2;
