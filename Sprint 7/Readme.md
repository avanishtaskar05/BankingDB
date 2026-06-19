CREATE TABLE Department
(  
    Department_ID INT PRIMARY KEY,  
    Department_Name VARCHAR(50),     
    Location VARCHAR(50)  
);

CREATE TABLE Employee   
(  
    Employee_ID INT PRIMARY KEY,  
    Employee_Name VARCHAR(100),  
    Salary DECIMAL(10,2),  
    Department_ID INT,  
    FOREIGN KEY (Department_ID) REFERENCES Department(Department_ID)  
);

CREATE TABLE Project (  
    Project_ID INT PRIMARY KEY,  
    Project_Name VARCHAR(100),  
    Budget DECIMAL(12,2),      
    Employee_ID INT,  
    FOREIGN KEY (Employee_ID) REFERENCES Employee(Employee_ID)  
);

INSERT INTO Department VALUES
(101, 'Human Resources', 'Mumbai'),  
(102, 'Information Technology', 'Pune'),  
(103, 'Finance', 'Delhi'),  
(104, 'Marketing', 'Bangalore'),  
(105, 'Operations', 'Hyderabad');  

INSERT INTO Employee VALUES  
(1, 'Amit Sharma', 65000, 102),  
(2, 'Priya Patel', 58000, 101),  
(3, 'Rahul Verma', 72000, 103),  
(4, 'Sneha Joshi', 60000, 104),  
(5, 'Vikas Singh', 68000, 105);  


INSERT INTO Project VALUES  
(201, 'Banking Analytics', 500000, 1),  
(202, 'HR Portal', 250000, 2),  
(203, 'Financial Dashboard', 400000, 3),  
(204, 'Digital Campaign', 300000, 4),  
(205, 'Supply Chain System', 450000, 5);  

Using Select and Aggregate Functions  
_________________________________________________________________
select count(*) as total_count from department;

select count(*) as total_count from department  
where location="Mumbai";  

select count(*) as total_count from department  
where location in ("Mumbai";"Pune");  

select count(*) as total_count from department    
where salary between 50000 and 70000;   

select count(*) as total_count from department     
where salary not between 50000 and 70000;  

select avg(salary) from employee;  

select empployee_name from employee  
where avg(salary) > 50000;  

selecct employee_name,max(salary) as max_salary from employee  
group by employee_name;  

select * from project  
where project_name="Supply Chain System" and budge > 50000;  
  
Using Join  
_________________________________________________________________  
select dept.department_name,dept.location,  
emp.employee_name,emp.salary  
from department dept  
join employee  emp  
on dept.department_id = emp.department_id;  
  
Using Join with Group By  
_________________________________________________________________  
select dept.department_name,max(emp.salary) as max_salary    
from department dept    
join employee emp  
on dept.department_id = emp.department_id  
group by dept.department_name;  
