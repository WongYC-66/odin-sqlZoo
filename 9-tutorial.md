1.
SELECT count(*)
FROM stops

2.
SELECT id
FROM stops
WHERE name = 'Craiglockhart'

3.
SELECT id, name
FROM route
JOIN stops ON stops.id = route.stop
WHERE num = 4 AND company = 'LRT'
ORDER BY pos

4.
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) >= 2

5.
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = 149

6.
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' and stopb.name = 'London Road'


7.
SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Haymarket' and stopb.name = 'Leith'


8.
SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' and stopb.name = 'Tollcross'


9.
SELECT stopb.name, b.company, b.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart'

10.
SELECT a.num, a.company,  stops.name,  d.num, d.company
FROM route AS a 
JOIN route AS b ON (a.company=b.company AND a.num=b.num)
JOIN stops ON (b.stop = stops.id)
JOIN route AS c on (c.stop = stops.id)
JOIN route AS d ON (c.company=d.company AND c.num=d.num)

WHERE a.stop = (SELECT id FROM stops WHERE name = 'Craiglockhart')
AND d.stop = (SELECT id FROM stops WHERE name = 'Lochend')

ORDER BY a.num, a.company, stops.name, d.num



