1.
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')

2.
SELECT name FROM world
  WHERE continent = 'Europe'
AND (gdp/population) >
     (SELECT (gdp/population) FROM world
      WHERE name='United Kingdom')

3.
SELECT name, continent FROM world
  WHERE continent in (SELECT continent FROM world
  WHERE name in ('Argentina', 'Australia')
)

4.
SELECT name, population FROM world
WHERE population < (SELECT population FROM world WHERE name = 'Germany')
AND population > (SELECT population FROM world WHERE name = 'United Kingdom')

5.
SELECT name, 
CONCAT(ROUND(population / (SELECT population FROM world WHERE name = 'Germany') * 100, 0),'%')
AS percentage 
FROM world
WHERE continent = 'Europe'

6.
SELECT name FROM world
WHERE gdp > (SELECT MAX(gdp) FROM world
WHERE continent = 'Europe')

7.
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)

8.
SELECT continent, name FROM world x
WHERE name =
    (SELECT name FROM world y
        WHERE y.continent=x.continent
        LIMIT 1
     )

9.
SELECT name, continent, population FROM world x
WHERE continent IN (
  SELECT continent FROM world y
  GROUP BY continent
  HAVING MIN(population <= 25000000)
)

10.
SELECT name, continent FROM world x
WHERE population / 3 > ALL
    (SELECT y.population FROM world y
        WHERE y.continent=x.continent
        AND x.name <> y.name
     )
or

SELECT name, continent FROM world x
WHERE population > ALL
    (SELECT y.population * 3 FROM world y
        WHERE y.continent=x.continent
        AND x.name <> y.name
     )