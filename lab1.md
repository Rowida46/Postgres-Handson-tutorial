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

2- 

```sql
 CREATE TABLE stubject (
    id           int PRIMARY KEY not NULL ,
    name         varchar(50) not NULL, 
    description        varchar(100),
    max_score     smallint
);
```


3- 

```sql
create table student_phone(std_id int not null references student , phone_number varchar(12), primary key(phone_number, std_id));
CREATE TABLE

```


4- 
```sql
create table student_subject(subj_id int ,std_id int, primary key(std_id, subj_id));
CREATE TABLE
```


5- 
```sql
create table track_subjects(subj_id int ,track_id int, primary key(track_id, subj_id));
CREATE TABLE
```
