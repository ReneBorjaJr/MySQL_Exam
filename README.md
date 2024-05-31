# MySQL_Exam
```sql
-- My Table
mysql> select * from movies;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
+-------------------+---------+-------------+------------+--------+

-- Add two more movies of your choosing to the table.
mysql> INSERT INTO movies
    -> VALUES ('Godzilla vs Kong', 113, 'Sci-Fi', 6.3, 'PG-13'),
    -> ('John Wick', 101, 'Action', 7.4, 'R');

mysql> select * from movies;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| Godzilla vs Kong  |     113 | Sci-Fi      |        6.3 | PG-13  |
| John Wick         |     101 | Action      |        7.4 | R      |
+-------------------+---------+-------------+------------+--------+

-- Create a query to find all movies in the Sci-Fi genre.
mysql> select title
    -> from movies
    -> where Genre = 'Sci-Fi'
    -> ;
+-------------------+
| title             |
+-------------------+
| Howard the Duck   |
| Starship Troopers |
| Godzilla vs Kong  |
+-------------------+

-- Create a query to find all films that scored at least a 6.5 on IMDB
mysql> select *
    -> from movies
    -> where imdb_score >= 6.5;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| John Wick         |     101 | Action      |        7.4 | R      |
+-------------------+---------+-------------+------------+--------+

-- For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long.
mysql> select *
    -> from movies
    -> where runtime < 100 AND (rating = 'PG' OR rating = 'G');
+---------------+---------+-----------+------------+--------+
| Title         | Runtime | Genre     | IMDB_Score | Rating |
+---------------+---------+-----------+------------+--------+
| Spaceballs    |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc. |      92 | Animation |        8.1 | G      |
+---------------+---------+-----------+------------+--------+

-- Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres.
mysql> select AVG(runtime), genre
    -> from movies
    -> where imdb_score < 7.5
    -> group by genre;
+--------------+--------+
| AVG(runtime) | genre  |
+--------------+--------+
|     117.3333 | Sci-Fi |
|      83.0000 | Horror |
|      96.0000 | Comedy |
|     101.0000 | Action |
+--------------+--------+

-- There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R.
mysql> UPDATE movies
    -> SET rating = "R"
    -> WHERE title = 'Starship Troopers';

mysql> select *
    -> from movies;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| Godzilla vs Kong  |     113 | Sci-Fi      |        6.3 | PG-13  |
| John Wick         |     101 | Action      |        7.4 | R      |
+-------------------+---------+-------------+------------+--------+

-- Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query.
mysql> ALTER TABLE movies
    -> ADD ID INT PRIMARY KEY AUTO_INCREMENT
    -> FIRST;

mysql> select * from movies;
+----+-------------------+---------+-------------+------------+--------+
| ID | Title             | Runtime | Genre       | IMDB_Score | Rating |
+----+-------------------+---------+-------------+------------+--------+
|  1 | Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
|  2 | Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
|  3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
|  4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|  5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|  6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
|  7 | Godzilla vs Kong  |     113 | Sci-Fi      |        6.3 | PG-13  |
|  8 | John Wick         |     101 | Action      |        7.4 | R      |
+----+-------------------+---------+-------------+------------+--------+

mysql> select id, rating
    -> from movies
    -> where Genre LIKE 'H%' OR genre like 'D%';
+----+--------+
| id | rating |
+----+--------+
|  2 | TV-14  |
|  4 | R      |
+----+--------+

-- This time let's find the average, maximum, and minimum IMDB score for movies of each rating.
mysql> select AVG(imdb_score) AS 'Average Score', MAX(imdb_score) AS 'Max Score', MIN(imdb_score) AS 'Min score', Rating
    -> from movies
    -> group by rating;
+---------------+-----------+-----------+--------+
| Average Score | Max Score | Min score | Rating |
+---------------+-----------+-----------+--------+
|       5.85000 |       7.1 |       4.6 | PG     |
|       4.70000 |       4.7 |       4.7 | TV-14  |
|       7.53333 |       8.0 |       7.2 | R      |
|       8.10000 |       8.1 |       8.1 | G      |
|       6.30000 |       6.3 |       6.3 | PG-13  |
+---------------+-----------+-----------+--------+

-- That last query isn't very informative for ratings that only have 1 entry. Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing.
mysql> select COUNT(rating) AS 'Movies per rating', rating
    -> from movies
    -> GROUP BY rating
    -> HAVING COUNT(rating) > 1;
+-------------------+--------+
| Movies per rating | rating |
+-------------------+--------+
|                 2 | PG     |
|                 3 | R      |
+-------------------+--------+



