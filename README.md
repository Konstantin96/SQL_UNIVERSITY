create table Groups(
id_group int NOT NULL identity(1,1) PRIMARY KEY,
Name_group varchar(200) UNIQUE
)

create table Family_polozheniye(
id_Family_polozheniye int NOT NULL identity(1,1) PRIMARY KEY,
Name varchar(100)
)

create table Students(
id_sudent int NOT NULL identity(1,1) PRIMARY KEY,
LastName_Student varchar(200),
FirstName_Student varchar(200),
Otchestvo_Student varchar(200),
group_id int REFERENCES Groups(id_group),
kurs int CHECK (kurs=10)
)

create table Teachers(
id_teacher int NOT NULL identity(1,1) PRIMARY KEY,
LastName_Teacher varchar(200),
FirstName_Teacher varchar(200),
Otchestvo_Teacher varchar(200),
Telephone_num char(11) UNIQUE,
Address_teacher varchar(150),
Family_polozheniye_Teacher int REFERENCES Family_polozheniye(id_Family_polozheniye)
) 
 

create table Uspevaemost_Student(
id_Uspevaemost_Student int NOT NULL identity(1,1) PRIMARY KEY,
id_student int REFERENCES Students(id_sudent),
procent_uspeva int CHECK (procent_uspeva=100)
)

create table Poseshaemost_Student(
id_Uspevaemost_Student int NOT NULL identity(1,1) PRIMARY KEY,
id_sudent int REFERENCES Students(id_sudent),
id_teacher int REFERENCES Teachers(id_teacher),
procent_poseshaemost int CHECK (procent_poseshaemost=100)
)

create table subjects(
id_subject int NOT NULL identity(1,1) PRIMARY KEY,
subject_name varchar (150)
)

create table teacher_subjects(
id_teacher_subjects int NOT NULL identity(1,1) PRIMARY KEY,
id_subjects int REFERENCES subjects(id_subject) NOT NULL ,
id_teacher int REFERENCES Teachers(id_teacher)
)

create table schedule(
id_schedul int NOT NULL identity(1,1) PRIMARY KEY,
teacher_subjects_id int REFERENCES teacher_subjects(id_teacher_subjects),
group_id int REFERENCES Groups(id_group),
schedule time
)
-_-_CREATE GROUP_-_-
INSERT INTO Groups(Name_group) values('smp_172.1')
INSERT INTO Groups(Name_group) values('smp_172.2')

-_-_CREATE Student_-_-
INSERT INTO Students(LastName_Student,FirstName_Student,Otchestvo_Student,group_id,kurs)
 values('Klyukin','Konstantin','Vladimirovich',1,2)

INSERT INTO Students(LastName_Student,FirstName_Student,Otchestvo_Student,group_id,kurs)
 values('Ivanova','Alexandra','Yurievna',2,2)

INSERT INTO Students(LastName_Student,FirstName_Student,Otchestvo_Student,group_id,kurs)
 values('Vasin','Ivan','Valentinovich',1,2)

INSERT INTO Students(LastName_Student,FirstName_Student,Otchestvo_Student,group_id,kurs)
 values('Zyakin','Vladislav','Semenovich',2,2)

 -_-_CREATE Family_polozheniye-_-
 INSERT INTO Family_polozheniye(Name) values('Holost')
 INSERT INTO Family_polozheniye(Name) values('Pomolvlen')
 INSERT INTO Family_polozheniye(Name) values('Vlyblen')
 INSERT INTO Family_polozheniye(Name) values('loneliness')

-_-_CREATE Teacher_-_-
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('Yancey', 'Vanichkov', 'Gardner', '2296505899', '829 Annamark Way',1);
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('Doretta', 'McIver', 'Cyril', '2748987721', '7764 Hoffman Street',4);
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('Amity', 'MacDonough', 'Adolphus', '2104544602', '01778 New Castle Road',2);
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('Sholom', 'Sambedge', 'Lambert', '0358300819', '518 Barnett Plaza',3);
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('Wang', 'MacGhee', 'Matt', '8358390629', '42 Fairfield Lane',1);

-_-_CREATE subjects-_-
insert into subjects (subject_name) values ('Math')
insert into subjects (subject_name) values ('Fizik')
insert into subjects (subject_name) values ('Informatika')
insert into subjects (subject_name) values ('History')
insert into subjects (subject_name) values ('Biography')

-_-_CREATE teacher_subjects-_-
insert into teacher_subjects (id_subjects, id_teacher) values (1,2);
insert into teacher_subjects (id_subjects, id_teacher) values (2,3);
insert into teacher_subjects (id_subjects, id_teacher) values (3,1);
insert into teacher_subjects (id_subjects, id_teacher) values (4,5);
insert into teacher_subjects (id_subjects, id_teacher) values (5,4);

-_-_CREATE schedule-_-
insert into schedule (teacher_subjects_id, group_id,schedule) values (1,1,'900');
insert into schedule (teacher_subjects_id, group_id,schedule) values (2,2,'900');
insert into schedule (teacher_subjects_id, group_id,schedule) values (3,1,'1100');
insert into schedule (teacher_subjects_id, group_id,schedule) values (4,2,'1100');
insert into schedule (teacher_subjects_id, group_id,schedule) values (1,2,'1300');
insert into schedule (teacher_subjects_id, group_id,schedule) values (2,1,'1300');

-_-_CREATE Uspevaemost_Student-_-
insert into Uspevaemost_Student (id_student, procent_uspeva) values (1,100);
insert into Uspevaemost_Student (id_student, procent_uspeva) values (2,95);
insert into Uspevaemost_Student (id_student, procent_uspeva) values (3,80);
insert into Uspevaemost_Student (id_student, procent_uspeva) values (4,50);

-_-_CREATE Poseshaemost_Student-_-
insert into Poseshaemost_Student (id_sudent, id_teacher,procent_poseshaemost) values (1,2,90);
insert into Poseshaemost_Student (id_sudent, id_teacher,procent_poseshaemost) values (2,4,100);
insert into Poseshaemost_Student (id_sudent, id_teacher,procent_poseshaemost) values (3,5,50);
insert into Poseshaemost_Student (id_sudent, id_teacher,procent_poseshaemost) values (4,1,70);

1. Выбрать всех студентов определенной группы.
SELECT  FROM Students WHERE group_id=2 

2. Выбрать преподавателей, которые читают пары в определенной группе
SELECT LastName_Teacher,FirstName_Teacher FROM Teachers,schedule WHERE group_id=1 AND teacher_subjects_id=1

3. Выбрать всех студентов, у которых читает определенный преподаватель
Select id_sudent,LastName_Student,FirstName_Student,group_id,LastName_Teacher,FirstName_Teacher FROM Students,Teachers WHERE id_teacher=1

SELECT  FROM schedule
SELECT  FROM teacher_subjects
4. Выбрать всех студентов с определенной фамилией
SELECT  FROM Students WHERE LastName_Student LIKE '%Klyukin%'

5. Изменить группу определенному студенту
UPDATE Students SET group_id = 2 WHERE LastName_Student LIKE '%Klyukin%'; 

6. Изменить № телефона определенного преподавателя 
UPDATE Teachers SET Telephone_num='2104544603' WHERE Telephone_num='2104544603'

7. Удалить определенного студента
DELETE FROM  Uspevaemost_Student WHERE id_student=4
DELETE FROM  Poseshaemost_Student WHERE id_sudent=4
DELETE FROM  Students WHERE id_sudent=4

8. Добавить нового преподавателя
insert into Teachers (LastName_Teacher, FirstName_Teacher, Otchestvo_Teacher, Telephone_num, Address_teacher,Family_polozheniye_Teacher) values ('gdsgd', 'Vangdfgdichkov', 'fgdgdfg', '575757', '829 57 gdf',1);

9. Добавить в таблицу студентов поле № телефона
ALTER TABLE Students ADD telephone char(11)

10. Установить всем студентам номер телефона 123456
UPDATE Students SET telephone = '123456' WHERE telephone is null 
select  FROM Students
