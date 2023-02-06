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
