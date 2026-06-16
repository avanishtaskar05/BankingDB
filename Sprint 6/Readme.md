**log_db**
____________________________________________________________________
create database if not exists log_db;
use log_db;
____________________________________________________________________
--creating table dim_learners

create table dim_learners (
learner_id int primary key auto_increment unique,
name varchar(20) not null,
learner_age int check(learner_age between 10 and 40) not null,
learner_gender enum("Male","Female","Other") default "Male",
learner_city varchar(30) not null);

____________________________________________________________________
--rename column name to learner_name

alter table dim_learners
rename column name to learner_name;

____________________________________________________________________
--creating table dim_trainers

create table dim_trainers (
trainer_id int primary key auto_increment unique,
trainer_name varchar(20) not null,
trainer_age int check(trainer_age between 10 and 40) not null,
trainer_gender enum("Male","Female","Other") default "Male",
trainer_city varchar(30) not null),
learner_id int,
foreign key (learner_id) references dim_learners(learner_id));
____________________________________________________________________
--creating table dim_ratings

create table dim_ratings(
learner_id int,
trainer_id int,
foreign key (learner_id) references learners (learner_id),
foreign key (trainer_id) references trainers (trainer_id)
learner_rating int check(learner_rating between 1 and 5),
trainer_rating int check(trainer_rating between 1 and 5),
learner_feedback tinytext,
trainer_feedback tinytext,
);

____________________________________________________________________
--inserting values into dim_learners

INSERT INTO Learners
(learner_id, learner_name, learner_age, learner_gender, learner_city)
VALUES
(1, 'Aarav', 22, 'Male', 'Mumbai'),
(2, 'Sneha', 19, 'Female', 'Pune'),
(3, 'Rohan', 25, 'Male', 'Nashik'),
(4, 'Priya', 21, 'Female', 'Nagpur'),
(5, 'Karan', 30, 'Male', 'Thane'));

____________________________________________________________________
--inserting values into dim_trainers

INSERT INTO dim_trainers
(trainer_id,trainer_name, trainer_age, trainer_gender, trainer_city, learner_id)
VALUES
(1,'Rajesh', 35, 'Male', 'Mumbai', 1),
(2,'Priya', 29, 'Female', 'Pune', 2),
(3,'Amit', 32, 'Male', 'Nashik', 3),
(4,'Sneha', 27, 'Female', 'Nagpur', 4),
(5,'Vikas', 38, 'Male', 'Thane', 5),

____________________________________________________________________
--inserting values into dim_ratings

INSERT INTO dim_ratings
(learner_id, trainer_id, learner_rating, trainer_rating, learner_feedback, trainer_feedback)
VALUES
(1, 1, 5, 4, 'Excellent trainer', 'Very dedicated learner'),
(2, 2, 4, 5, 'Good explanation', 'Quick learner'),
(3, 3, 3, 4, 'Average session', 'Participates actively'),
(4, 4, 5, 5, 'Outstanding guidance', 'Excellent performance'),
(5, 5, 4, 3, 'Helpful trainer', 'Needs more practice'));

____________________________________________________________________
--Using join two get learenr_name, learner_age, trainer_name and trainer_age when learner_id = trainer_id by joining two tables

select l.learner_name,l.learner_age,
t.trainer_name,t.trainer_age
from dim_learners l
join on dim_trainers t
where l.learner_id = t.trainer_id;
