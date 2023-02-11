1- Create Table called Deleted_Students which will hold the deleted students info (same columns as in student tables)

```SQL

----------------- Function triggres

CREATE or REPLACE Function student_logs()
RETURNS TRIGGER 
AS $$
BEGIN
    insert into studentlogs values(OLD.id,OLD.email, concat('this record was found at',now()));
    return OLD; 
END;
$$ LANGUAGE plpgsql;

-- Creating trigger

CREATE TRIGGER delete_student_logs AFTER Delete
ON student for EACH row EXECUTE
PROCEDURE student_logs();
```

- _delete record from student table_ and view result from `studentlogs` table that hold logs related to student table
![image](https://user-images.githubusercontent.com/52299389/218282636-28593bf6-3335-47d4-b619-54ac9e8fbd83.png)

---

2- Create trigger to save the deleted student from Student table to
Deleted_Students

```sql


CREATE or REPLACE Function delete_std_logs()
RETURNS TRIGGER 
AS $$
BEGIN
    insert into Deleted_Students values(OLD.id,OLD.email,OLD.address, OLD.Track_id);
    return OLD; 
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER delete_std_logs AFTER Delete
ON student for EACH row EXECUTE
PROCEDURE student_logs();
```

--- 

3- try to delete student from students table and check the
Deleted_Students if it contain the deleted students or not

```sql

CREATE or REPLACE Function search_ondelete_logs()
RETURNS TRIGGER 
AS $$
BEGIN
    select * from studentlogs where id = OLD.id;
    insert into studentlogs values(OLD.id,OLD.email, concat('this record was found at',now()));
    return null; 
END;
$$ LANGUAGE plpgsql;


CREATE TRIGGER searcch_ondelete_std_logs AFTER Delete
ON student for EACH row EXECUTE
PROCEDURE student_logs();


```
