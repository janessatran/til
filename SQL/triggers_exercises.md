Datatables from [here](https://lagunita.stanford.edu/c4x/DB/Constraints/asset/socialdata.html).

1. Write a trigger that makes new students named 'Friendly' automatically like everyone else in their grade. That is, after the trigger runs, we should have ('Friendly', A) in the Likes table for every other Highschooler A in the same grade as 'Friendly'.
```sql
CREATE TRIGGER FriendlyTrigger
AFTER INSERT ON Highschooler
WHEN new.name = "Friendly"
BEGIN
    INSERT INTO Likes SELECT new.id, h.id FROM Highschooler h
    WHERE new.grade = h.grade AND not new.id = h.id;
END
```



2. Write one or more triggers to manage the grade attribute of new Highschoolers. If the inserted tuple has a value less than 9 or greater than 12, change the value to NULL. On the other hand, if the inserted tuple has a null value for grade, change it to 9. 
```sql
CREATE TRIGGER g
AFTER INSERT ON Highschooler
BEGIN
    UPDATE Highschooler SET grade = NULL WHERE id = new.id and (new.grade < 9 or new.grade > 12);
    UPDATE Highschooler SET grade = 9 WHERE id = new.id and (new.grade is NULL);
END
```



3. Write one or more triggers to maintain symmetry in friend relationships. Specifically, if (A,B) is deleted from Friend, then (B,A) should be deleted too. If (A,B) is inserted into Friend then (B,A) should be inserted too. Don't worry about updates to the Friend table. 
```sql
CREATE TRIGGER deleteFriendTrigger
AFTER DELETE ON Friend
BEGIN
    DELETE FROM Friend WHERE id1=old.id2 AND id2=old.id1;
END

|

CREATE TRIGGER insertFriendTrigger
AFTER INSERT ON Friend
BEGIN
    INSERT INTO Friend VALUES (new.id2, new.id1);
END
```



4. Write a trigger that automatically deletes students when they graduate, i.e., when their grade is updated to exceed 12. 
```sql
CREATE TRIGGER GradTrigger
AFTER UPDATE ON Highschooler
WHEN new.grade > 12
BEGIN
    DELETE FROM Highschooler WHERE id = new.id;
END
```



5. Write a trigger that automatically deletes students when they graduate, i.e., when their grade is updated to exceed 12 (same as Question 4). In addition, write a trigger so when a student is moved ahead one grade, then so are all of his or her friends. 
```sql
CREATE TRIGGER GradTrigger
AFTER UPDATE ON Highschooler
WHEN new.grade > 12
BEGIN
    DELETE FROM Highschooler WHERE id = new.id;
END

|

CREATE TRIGGER gt2
AFTER UPDATE ON Highschooler
WHEN new.grade = old.grade + 1
BEGIN
    UPDATE Highschooler
    SET grade = grade + 1 
    WHERE id in (SELECT id2 FROM Friend WHERE id1 = new.id);
END    
```



6. Write a trigger to enforce the following behavior: If A liked B but is updated to A liking C instead, and B and C were friends, make B and C no longer friends. Don't forget to delete the friendship in both directions, and make sure the trigger only runs when the "liked" (ID2) person is changed but the "liking" (ID1) person is not changed. 
```sql
CREATE TRIGGER a
AFTER UPDATE ON Likes
WHEN new.id2 <> old.id2 and new.id1 == old.id1 
     and 
     exists(select * from Friend where id1 = new.id2 and id2 = old.id2)
BEGIN
    DELETE FROM Friend
    WHERE (id2 = old.id2 and id1 = new.id2) or (id1 = old.id2 and id2 = new.id2);
END
```
