1.
SELECT id, title
 FROM movie
 WHERE yr=1962

2.
SELECT yr
 FROM movie
 WHERE title="Citizen Kane"

3.
SELECT id, title, yr
 FROM movie
 WHERE title LIKE "%Star Trek%"
 ORDER BY yr

4.
SELECT id
 FROM actor
 WHERE name = 'Glenn Close'

5.
SELECT id 
FROM movie
WHERE title = 'Casablanca'

6.
SELECT name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE movieid = 11768


7.
SELECT name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE movie.title = 'Alien'

8.
SELECT title
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE name = 'Harrison Ford'

9.
SELECT title
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE name = 'Harrison Ford' AND casting.ord <> 1

10.
SELECT title, name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE yr= 1962 AND casting.ord = 1

11.
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2

12.
SELECT title, name FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE casting.ord = 1 AND movie.id in (
 SELECT movie.id FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
  WHERE name = 'Julie Andrews'
)


13.
SELECT name
FROM casting
JOIN actor ON actor.id = casting.actorid
WHERE casting.ord = 1

GROUP BY actorid
HAVING COUNT(*) >= 15
ORDER BY name

14.
SELECT title, COUNT(*)
FROM movie
JOIN casting ON casting.movieid = movie.id
WHERE yr = 1978
GROUP BY id
ORDER BY COUNT(*) DESC, title

15.
SELECT DISTINCT name
FROM casting
JOIN actor ON actor.id = casting.actorid
WHERE actor.id <> (
 SELECT id
 FROM actor
 WHERE name = 'Art Garfunkel'
)
AND movieid in (
 SELECT movieid 
 FROM casting
 WHERE actorid = (
   SELECT id 
   FROM actor
   WHERE name = 'Art Garfunkel'
 )
)

