1- Insert new student and his score in exam in different subjects as transaction and save it

```SQL

BEGIN;
insert into student values (6,'newStd', 'rowida@gmail.com', 'addres', 1);
insert into exam_details values (6, 90,  4);
insert into exam_details values (6, 90,  3);

COMMIT;

```

---

2- Insert new students and his score in exam in different subjects as transaction and rollback it

```sql
BEGIN;
insert into student values (7,'newStd', 'rowida@gmail.com', 'addres', 1);
insert into exam_details values (7, 90,  4);
insert into exam_details values (7, 90,  3);

ROLLBACK;
```
---

3- Create a view for student names with their Tracks names which is belong to it.

```sql
create view student_tracks as
select std.name, track.name as track_name 
from student  std join track 
on track.id = std.track_id;
```
![image](https://user-images.githubusercontent.com/52299389/217234065-858f59b7-cfee-411f-9ba7-78a594d7772f.png)

---


4- Create a view for Tracks names and the subjects which is belong/study to it.

```SQL

CREATE VIEW track_subjects_view as 
select sbj.name as subject_name , track.name as track_name
from subject sbj join track_subjects 
on track_subjects.subject_id = sbj.id
join track on
 track_subjects.track_id = track.id;
```
![image](https://user-images.githubusercontent.com/52299389/217236978-6406cf2f-1aea-476a-b996-07ea47fc9d62.png)


---


5- Create a view for student names with their subject's names which will study.

```SQL

CREATE VIEW student_subject_view as
select std.name  as student_name , sbj.name as subject_name  from student std 
join student_subjects on student_subjects.student_id = std.id
join subject sbj on sbj.id = student_subjects.subject_id;

```
![image](https://user-images.githubusercontent.com/52299389/217238133-9e2eacb8-2a12-48bb-b006-8d022da9a518.png)


--- 


6- Create a view for all students name (Full Name) with their score in each subject and its date.

```SQL

CREATE VIEW student_exam_details as
select std.name  as student_Full_name , sbj.name as subject_name , exam_details.score 
from student std 
join exam_details on exam_details.student_id = std.id
join subject sbj on sbj.id = exam_details.subject_id;

```
![image](https://user-images.githubusercontent.com/52299389/217238915-e480c4cf-d650-46a6-b948-c377b22e58fe.png)

---


7. Create a temporary view for all subjects with their max_score

```sql

CREATE TEMPORARY VIEW subjects_score as
select sbj.name as subject_name , exam_details.score 
from subject sbj
join exam_details  on sbj.id = exam_details.subject_id;

```

![image](https://user-images.githubusercontent.com/52299389/217240827-0398eae2-7312-4329-9159-d972b1ac297d.png)


---- 


9- Create user and give him all privileges.


```nano
local   all             all                                     trust

```
---

10 -( from Q.6) Display the date of exam as the following: day 'month name' year.

```SQL
select TO_CHAR(AGE(now(),birthdate) , 'yy') from student;
```

![image](https://user-images.githubusercontent.com/52299389/217249365-e5354d02-3a74-4654-b29c-72a14357788e.png)

![image](https://user-images.githubusercontent.com/52299389/217249229-026154de-12af-4751-a80a-cb58337ad261.png)

11- Display name and age of each students


![image](https://user-images.githubusercontent.com/52299389/217246344-3b0a59e8-6a68-47d0-98dd-7232086dcad5.png)

--


12- Display the name of students with their Rounded score in each subject

![image](https://user-images.githubusercontent.com/52299389/217250073-47f331fa-660a-46e5-9448-043ccf3d0c23.png)


---


13- Display the name of students with the year of Birthdate

![image](https://user-images.githubusercontent.com/52299389/217250526-88a783cf-45b1-484a-993f-f7da361f533e.png)


14- Add new exam result, in date column use NOW() function;
![image](https://user-images.githubusercontent.com/52299389/217250774-fc53f611-383d-4e56-aecd-4fbd7df55a33.png)


15- Create database called ITI, and create different schema and Tables inside this
scheme.

_to create a schema_
```SQL
CREATE SCHEMA Tracks;
```

![image](https://user-images.githubusercontent.com/52299389/217251725-4e267758-7de9-41c0-a862-8d9851d69157.png)
