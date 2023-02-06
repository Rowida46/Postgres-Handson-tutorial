1- Create table student

```sql
CREATE TABLE student (
    id           int PRIMARY KEY not NULL ,
    name         varchar(50) not NULL, 
    email        varchar(50) NOT NULL,
    address      varchar(100) ,
        track_id     int,
    CONSTRAINT track_id FOREIGN KEY(track_id)
        REFERENCES track(id)
);
```
--- 

2- Create Subject table

```sql
 CREATE TABLE subject (
    id           int PRIMARY KEY not NULL ,
    name         varchar(50) not NULL, 
    description        varchar(100),
    max_score     smallint
);
```

--- 

3- _student_phone_ Table

```sql
create table student_phone(std_id int not null references student ,
phone_number varchar(12),
primary key(phone_number, std_id)
);
```
---


4-  _student_subjects_ Table.

```sql 
create table student_subjects(
    student_id int  references student(id),
    subject_id int references subject(id),
    primary key(student_id, subject_id)
);
```
---

5- _track_subjects_ Table 

```sql
create table track_subjects(
    track_id int  references track(id)
    , subject_id int references subject(id) ,
    primary key(track_id, subject_id)
);
```
---

6 - _exam_details_ Table.

```sql
create table exam_details(student_id int references student(id), score decimal, subject_id int references subject(id) , primary key(student_id, subject_id)); 
```

---

7- _exam_ Table.

```sql
create table exam (id int primary key, date date);
```
-----------

# DML Queries

- Insert  Student table.

![Screenshot from 2023-02-06 20-43-17](https://user-images.githubusercontent.com/52299389/217059037-4ae97a61-748d-4c51-8383-8a8c4281d775.png)


- Insert  Subject table.

![image](https://user-images.githubusercontent.com/52299389/217059301-c6a85863-31d2-4135-ab95-73c6938c6462.png)


- Insert into _Track_ table..

![image](https://user-images.githubusercontent.com/52299389/217059563-f128b3eb-98d7-4e2e-b838-9f5a2bace7f7.png)

- Insert into _track_subjects_ an _student_subject_ tables

![image](https://user-images.githubusercontent.com/52299389/217060119-ea22811a-e92f-4f2d-aec2-69488d4d0008.png)

- Insert into _exam_ table

![image](https://user-images.githubusercontent.com/52299389/217060959-b4abb862-fb5a-434c-bc7a-fc7caafef1c7.png)

- Insert into _exam_details_ table

![image](https://user-images.githubusercontent.com/52299389/217061094-54230819-77d6-4336-8c78-7bbf078018dd.png)



