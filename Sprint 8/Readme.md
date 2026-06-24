Creating database posts_db  

---------------------------------------------  
create database if not exists posts_db;    

--Create table posts  

---------------------------------------------  
create table posts  ( 
post_id int primary key unique,  
likes int not null  
);  

--Inserting into posts  

---------------------------------------------  
insert into posts values (1,2131),  
(2,312),  
(3,3242);  

--Limit and offset  

---------------------------------------------  
select post_id,likes from posts limit 2 offset 1;  

--Winodws Function Sum with Over   

---------------------------------------------  
select post_id,likes,sum(likes) over() as total_likes;
