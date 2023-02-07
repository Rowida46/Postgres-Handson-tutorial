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
