Datatables can be found [here](https://lagunita.stanford.edu/c4x/DB/Views/asset/viewmoviedata.html)

1. Write an instead-of trigger that enables updates to the title attribute of view LateRating. 

Policy: Updates to attribute title in LateRating should update Movie.title for the corresponding movie. (You may assume attribute mID is a key for table Movie.) Make sure the mID attribute of view LateRating has not also been updated -- if it has been updated, don't make any changes. Don't worry about updates to stars or ratingDate.

```sql
CREATE TRIGGER a
INSTEAD OF UPDATE of title ON LateRating
FOR EACH ROW
BEGIN
    UPDATE Movie set title = new.title 
    WHERE mID = new.mID;
END;
```

2. Write an instead-of trigger that enables updates to the stars attribute of view LateRating. 

Policy: Updates to attribute stars in LateRating should update Rating.stars for the corresponding movie rating. (You may assume attributes [mID,ratingDate] together are a key for table Rating.) Make sure the mID and ratingDate attributes of view LateRating have not also been updated -- if either one has been updated, don't make any changes. Don't worry about updates to title.

```sql
CREATE TRIGGER b
INSTEAD OF UPDATE of stars ON LateRating
FOR EACH ROW
BEGIN
    UPDATE Rating SET stars = new.stars
    WHERE mID = new.mID AND ratingDate = new.ratingDate;
END;
```

3. Write an instead-of trigger that enables updates to the mID attribute of view LateRating. 

Policy: Updates to attribute mID in LateRating should update Movie.mID and Rating.mID for the corresponding movie. Update all Rating tuples with the old mID, not just the ones contributing to the view. Don't worry about updates to title, stars, or ratingDate.

```sql
CREATE TRIGGER b
INSTEAD OF UPDATE OF mID ON LateRating
FOR EACH ROW
BEGIN
    UPDATE Rating SET mID = new.mID WHERE mID = old.mID;
    UPDATE Movie SET mID = new.MID where mID = old.mID;
END;
```

4. Finally, write a single instead-of trigger that combines all three of the previous triggers to enable simultaneous updates to attributes mID, title, and/or stars in view LateRating. Combine the view-update policies of the three previous problems, with the exception that mID may now be updated. Make sure the ratingDate attribute of view LateRating has not also been updated -- if it has been updated, don't make any changes.

```sql
CREATE TRIGGER allTrigger
INSTEAD OF UPDATE ON LateRating
FOR EACH ROW
WHEN old.mID IN (select mID from Rating where ratingDate = new.ratingDate)
BEGIN
  UPDATE Movie SET title = new.title, mID = new.mID
  WHERE old.mID = mID;
  UPDATE Rating SET stars = new.stars
  WHERE old.mID = mID and ratingDate = old.ratingDate;
  UPDATE Rating set mID = new.mID
  WHERE old.mID = mID;
END;
```

5. Write an instead-of trigger that enables deletions from view HighlyRated. 

Policy: Deletions from view HighlyRated should delete all ratings for the corresponding movie that have stars > 3.

```sql
CREATE TRIGGER m
INSTEAD OF DELETE ON HighlyRated
FOR EACH ROW
BEGIN
    DELETE FROM Rating
    WHERE mID = old.mID and stars > 3;
END;
```

6. Write an instead-of trigger that enables deletions from view HighlyRated. 

Policy: Deletions from view HighlyRated should update all ratings for the corresponding movie that have stars > 3 so they have stars = 3.

```sql
CREATE TRIGGER m
INSTEAD OF DELETE ON HighlyRated
FOR EACH ROW
BEGIN
    UPDATE Rating set stars = 3
    WHERE mID = old.mID and stars > 3;
END;
```

7. Write an instead-of trigger that enables insertions into view HighlyRated. 

Policy: An insertion should be accepted only when the (mID,title) pair already exists in the Movie table. (Otherwise, do nothing.) Insertions into view HighlyRated should add a new rating for the inserted movie with rID = 201, stars = 5, and NULL ratingDate.

```sql
CREATE TRIGGER m
INSTEAD OF INSERT ON HighlyRated
FOR EACH ROW
WHEN new.mID in (select mID FROM Movie WHERE mID = new.mID and title = new.title)
BEGIN
    INSERT INTO Rating VALUES(201, new.mID, 5, NULL);
END;
```

8. Correct (1/1 point) Review
Q8
1/1 point (graded)
Write an instead-of trigger that enables insertions into view NoRating. 

Policy: An insertion should be accepted only when the (mID,title) pair already exists in the Movie table. (Otherwise, do nothing.) Insertions into view NoRating should delete all ratings for the corresponding movie.

```sql
CREATE TRIGGER f
INSTEAD OF INSERT ON NoRating
FOR EACH ROW
WHEN new.mID in (SELECT mID from Movie where mId = new.mID and title = new.title)
BEGIN
    DELETE FROM Rating
    WHERE mId = new.mID;
END;
```

9. Write an instead-of trigger that enables deletions from view NoRating. 

Policy: Deletions from view NoRating should delete the corresponding movie from the Movie table.

```sql
CREATE TRIGGER b
INSTEAD OF DELETE ON NoRating
FOR EACH ROW
BEGIN
    DELETE FROM Movie 
    WHERE mID = old.mID and title = old.title;
END;
```

10. Write an instead-of trigger that enables deletions from view NoRating. 

Policy: Deletions from view NoRating should add a new rating for the deleted movie with rID = 201, stars = 1, and NULL ratingDate.

```sql
CREATE TRIGGER a 
INSTEAD OF DELETE ON NoRating
FOR EACH ROW
BEGIN
    INSERT INTO Rating VALUES(201, old.mID, 1, NULL);
END;
```

