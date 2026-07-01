create database if not exists post_db;  
use post_db;  


CREATE TABLE posts (  
    id INT,  
    likes INT  
);  

INSERT INTO posts (id, likes) VALUES  
(1, 150),  
(1, 120),  
(1, 120),  
(2, 200),  
(2, 180),  
(2, 150),  
(3, 250),  
(3, 250),  
(3, 100),  
(4, 180),  
(4, 160),  
(5, 150);  

--using sum()with over()  
________________________________________________________________________________________  
select id,likes,sum(likes) over(partition by id, order by likes desc) as rank from posts;  

--using dense_rank with over()
________________________________________________________________________________________   
select id,likes, dense_rank() over (order by likes desc) as rank from posts;   

--using rank with over()  
________________________________________________________________________________________   
select id,likes,rank() over (order by likes desc) as rank from posts;   
