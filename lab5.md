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

---

4 - Create trigger to prevent insert new Course with name length greater
than 20 chars;

```sql

CREATE or REPLACE Function handel_insert_newSubject()
RETURNS TRIGGER
AS $$ 
BEGIN
    if Length(NEW.name) > 20
    then 
    
        return NULL;
    else 
        return NEW;
    end if;
    
END;
$$ LANGUAGE plpgsql;


CREATE TRIGGER handel_insert_newSubject_trigger BEFORE insert
ON subject for EACH row EXECUTE
PROCEDURE handel_insert_newSubject();


```

_resurlt of excution_

![image](https://user-images.githubusercontent.com/52299389/218283543-0ffd17e2-2df1-41a6-9a69-2b0a28fcae42.png)


----

5- Create trigger to prevent update student names.

```SQL

CREATE or REPLACE Function prevent_update_std_name()
RETURNS TRIGGER
AS $$ 
BEGIN
    if OLD.name <> NEW.name 
    then 
        return NULL;
    else 
        return NEW;
    end if;
    
END;
$$ LANGUAGE plpgsql;

--- TRIGGER
CREATE TRIGGER prevent_update_std_name_trigger BEFORE UPDATE
ON student for EACH row EXECUTE
PROCEDURE prevent_update_std_name();

```

![image](https://user-images.githubusercontent.com/52299389/218283656-4ee55353-af03-4d9d-833d-61b32e7b4a86.png)


---

6- Create trigger to prevent update grades of students.

```sql

CREATE or REPLACE Function prevent_update_std_grads()
RETURNS TRIGGER
AS $$ 
BEGIN
    if OLD.score <> NEW.score 
    then 
        return NULL;
    else 
        return NEW;
    end if;
    
END;
$$ LANGUAGE plpgsql;

-- trgger on exam_details table
CREATE TRIGGER prevent_update_std_grads_trigger BEFORE UPDATE
ON exam_details for EACH row EXECUTE
PROCEDURE prevent_update_std_grads();

```

![image](https://user-images.githubusercontent.com/52299389/218283757-6cac95b8-8ecb-4dad-9b72-c7dad93540f1.png)


--- 

7- Create trigger to prevent user to insert or update Exam with Score
greater than 100 or less than zero

```SQL


CREATE or REPLACE Function prevent_exceed_max_grads()
RETURNS TRIGGER
AS $$ 
BEGIN
    if (NEW.score > 100 OR NEW.score < 0) 
    then 
        return NULL;
    else 
        return NEW;
    end if;
    
END;
$$ LANGUAGE plpgsql;


CREATE TRIGGER prevent_exceed_max_grads_trigger BEFORE UPDATE or insert
ON exam_details for EACH row EXECUTE
PROCEDURE prevent_exceed_max_grads();

```
![image](https://user-images.githubusercontent.com/52299389/218283910-56ba1f4d-75eb-41c7-89a1-2fdf4af37d95.png)


9- Create trigger to prevent any user to update/insert/delete to all
tables (Students, Exams, Tracks,..) after 7:00 PM


10 - Backup your Database to external file

```sh
pg_dump iti> lababackup.sql
```


11-  Backup your Student table to external file

```sh
Pg_dump iti -t student -f p > file.sql
```
