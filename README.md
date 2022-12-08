# my-exercises
SQL - список задач:

+ [1 задание](#1)
+ [2 задание](#2)
+ [3 задание](#3)
+ [4 задание](#4)
+ [5 задание](#5)
+ [6 задание](#6)
+ [7 задание](#7)
+ [8 задание](#8)
+ [9 задание](#9)
+ [10 задание](#10)

### 1 
[Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd](https://sql-ex.ru/learn_exercises.php?LN=1)

Решение: 
```sql
SELECT model, speed, hd FROM PC WHERE price < 500
```

### 2
[Найдите производителей принтеров. Вывести: maker](https://sql-ex.ru/learn_exercises.php?LN=2)

Решение:
```sql
SELECT maker FROM Product WHERE type = 'Printer' GROUP BY maker
```

### 3

[Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.](https://sql-ex.ru/learn_exercises.php?LN=3)

Решение:
```sql
SELECT model,ram,screen FROM Laptop WHERE price > 1000
```

### 4

[Найдите все записи таблицы Printer для цветных принтеров.](https://sql-ex.ru/learn_exercises.php?LN=4)

Решение: 
```sql
SELECT * FROM Printer WHERE color = 'y'
```

### 5 
[Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.](https://sql-ex.ru/learn_exercises.php?LN=5)

Решение:
```sql
SELECT model, speed, hd FROM PC WHERE ( cd = '12x' OR cd = '24x' ) AND price < 600
```

### 6
[Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.](https://sql-ex.ru/learn_exercises.php?LN=6)

Решение: 
```sql
SELECT DISTINCT maker, speed FROM laptop JOIN 
(SELECT * FROM product WHERE type='laptop')
this_table_1 ON laptop.model = this_table_1.model
WHERE hd >= 10
```

### 7
[Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).](https://sql-ex.ru/learn_exercises.php?LN=7)

Решение: 
```sql
SELECT DISTINCT pc.model, price FROM pc JOIN product on pc.model = product.model WHERE maker = 'B'
UNION 
SELECT DISTINCT laptop.model, price FROM laptop JOIN product on laptop.model = product.model WHERE maker = 'B'
UNION
SELECT DISTINCT printer.model, price FROM printer JOIN product on printer.model = product.model WHERE maker = 'B'
```

### 8
[Найдите производителя, выпускающего ПК, но не ПК-блокноты.](https://sql-ex.ru/learn_exercises.php?LN=8)

Решение: 
```sql
SELECT maker FROM product WHERE type = 'pc'
EXCEPT
SELECT maker FROM product WHERE type = 'laptop'
```

### 9
[Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker](https://sql-ex.ru/learn_exercises.php?LN=9)

Решение: 
```sql
SELECT DISTINCT product.maker FROM product JOIN pc on pc.model = product.model WHERE speed >= 450
```

### 10 
[Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price](https://sql-ex.ru/learn_exercises.php?LN=10)

Решение: 
```sql
SELECT DISTINCT model, price FROM printer
WHERE price = (SELECT MAX(price) FROM printer)
```

### 11
[Найдите среднюю скорость ПК.](https://sql-ex.ru/learn_exercises.php?LN=11)

Решение:
```sql
SELECT AVG(speed) AS Avg_speed FROM pc
```

### 12 
[Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.](https://sql-ex.ru/learn_exercises.php?LN=12)

Решение: 
``` sql
SELECT AVG(speed) AS Avg_speed FROM laptop WHERE price > 1000
```

### 13
[Найдите среднюю скорость ПК, выпущенных производителем A.](https://sql-ex.ru/learn_exercises.php?LN=13)

Решение:
```sql
SELECT DISTINCT AVG(pc.speed) AS Avg_speed FROM pc JOIN product on pc.model = product.model WHERE maker = 'A'
```
### 14 

[Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.](https://sql-ex.ru/learn_exercises.php?LN=14)

Решение: 
```sql
SELECT s.class, s.name, c.country
FROM ships s
JOIN classes c ON s.class = c.class
WHERE c.numGuns >= 10
```

### 15

[Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD](https://sql-ex.ru/learn_exercises.php?LN=15)

Решение: 
```sql
SELECT hd FROM pc GROUP BY (hd) HAVING COUNT(model) >= 2
```

### 16 

[Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.](https://sql-ex.ru/learn_exercises.php?LN=16)

Решение:
```sql
SELECT DISTINCT p1.model, p2.model, p1.speed, p1.ram
FROM pc p1, pc p2
WHERE p1.speed = p2.speed AND p1.ram = p2.ram AND p1.model > p2.model
```

### 17

[Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed](https://sql-ex.ru/learn_exercises.php?LN=17)

Решение:
```sql
SELECT DISTINCT product.type, laptop.model, laptop.speed
FROM laptop, product
WHERE speed < (SELECT MIN(speed) FROM pc)
AND product.type ='Laptop'
```

### 18 

[Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price](https://sql-ex.ru/learn_exercises.php?LN=18)

Решение: 
```sql
SELECT DISTINCT maker, price FROM product JOIN printer ON printer.model = product.model WHERE price = (SELECT MIN(price) FROM printer
WHERE color='y')
AND color='y'
```

### 19

[Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.](https://sql-ex.ru/learn_exercises.php?LN=19)

Решение:
```sql
SELECT maker, AVG(screen)
FROM product JOIN laptop ON product.model=laptop.model
GROUP BY maker
```

### 20 

[Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.](https://sql-ex.ru/learn_exercises.php?LN=20)

Решение: 
```sql
SELECT maker as Maker, COUNT(model) as Count_Model
FROM product
WHERE type='pc'
GROUP BY maker
HAVING COUNT(model)>=3
```
### 21

[Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT maker as Maker, MAX(price) as Max_price FROM product
JOIN pc ON product.model = pc.model
GROUP BY maker
```
### 22 

[Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT speed as Speed, AVG(price) as Price
FROM pc WHERE speed > 600
GROUP BY speed
```
### 23

[Найдите производителей, которые производили бы как ПК
со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц.
Вывести: Maker](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT DISTINCT maker
FROM product JOIN pc ON product.model=pc.model
WHERE speed>=750 AND maker IN
(SELECT maker
FROM product JOIN laptop ON product.model=laptop.model
WHERE speed>=750)
```

### 24

[Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT model 
FROM (
 SELECT model, price FROM pc
 UNION
 SELECT model, price FROM laptop
 UNION
 SELECT model, price FROM printer
) table1
WHERE price = (
 SELECT MAX(price) 
FROM (
  SELECT price FROM pc
  UNION
  SELECT price FROM laptop
  UNION
  SELECT price FROM Printer
  ) table2
 )
```
### 25

[Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT DISTINCT maker FROM product
WHERE model IN (
SELECT model FROM pc
WHERE ram = (SELECT MIN(ram)
  FROM pc
  )
AND speed = (
  SELECT MAX(speed)
  FROM pc
  WHERE ram = (
   SELECT MIN(ram)
   FROM pc
   )
  )
)
AND
maker IN (
SELECT maker
FROM product
WHERE type='printer'
)
```
### 26

[Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение: 
```sql
SELECT AVG(price) AS AVG_price FROM (SELECT model, price FROM PC
UNION ALL
SELECT model, price FROM Laptop) AS price
INNER JOIN product
ON price.model = product.model
WHERE maker = 'A'
```

### 27:

[Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.](https://sql-ex.ru/learn_exercises.php)

Решение:
```sql
SELECT maker as Maker, AVG(hd) as AVG
FROM product JOIN pc ON product.model=pc.model
WHERE maker IN (
SELECT maker
FROM product
WHERE type='printer'
)
GROUP BY maker
```

### 28:

[Используя таблицу Product, определить количество производителей, выпускающих по одной модели.](https://sql-ex.ru/learn_exercises.php?LN=28)

Решение:
```sql
SELECT COUNT(maker) as Quantity FROM 
(
SELECT maker FROM product GROUP BY maker HAVING COUNT(*) = 1
) this_table
```
### 29

[В предположении, что приход и расход денег на каждом пункте приема фиксируется не чаще одного раза в день [т.е. первичный ключ (пункт, дата)], написать запрос с выходными данными (пункт, дата, приход, расход). Использовать таблицы Income_o и Outcome_o.](https://sql-ex.ru/learn_exercises.php?LN=29)

Решение:
```sql
SELECT income_o.point, income_o.[date], inc, out FROM income_o LEFT JOIN outcome_o ON outcome_o.point = income_o.point
AND outcome_o.[date]=income_o.[date]
UNION
SELECT outcome_o.point, outcome_o.[date], inc, out FROM income_o RIGHT JOIN outcome_o ON
outcome_o.point = income_o.point AND outcome_o.[date] = income_o.[date]
```
### 30

[В предположении, что приход и расход денег на каждом пункте приема фиксируется произвольное число раз (первичным ключом в таблицах является столбец code), требуется получить таблицу, в которой каждому пункту за каждую дату выполнения операций будет соответствовать одна строка.
Вывод: point, date, суммарный расход пункта за день (out), суммарный приход пункта за день (inc). Отсутствующие значения считать неопределенными (NULL).](https://sql-ex.ru/learn_exercises.php?LN=30)

Решение:
```sql
SELECT point, [date], SUM(outs), SUM(incs) FROM
(SELECT point, [date], SUM(out) outs, null incs FROM outcome GROUP BY point, [date]
UNION
SELECT point, [date], null, SUM(inc) incs FROM income GROUP BY point, [date]) this_table GROUP BY point, [date]
```

### 31

[Для классов кораблей, калибр орудий которых не менее 16 дюймов, укажите класс и страну.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT class, country
FROM classes
WHERE bore>=16
```
### 32

[Одной из характеристик корабля является половина куба калибра его главных орудий (mw). С точностью до 2 десятичных знаков определите среднее значение mw для кораблей каждой страны, у которой есть корабли в базе данных.](https://sql-ex.ru/learn_exercises.php?LN=32)

Решение:
```sql
SELECT country, cast(avg(bore*bore*bore/2) as numeric(38,2)) FROM
(SELECT country, name, bore FROM ships sh JOIN classes c ON sh.class=c.class
union
SELECT country, ship, bore FROM outcomes o JOIN classes c ON o.ship = c.class) t1
GROUP BY country
```
### 33

[Укажите корабли, потопленные в сражениях в Северной Атлантике (North Atlantic). Вывод: ship.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:

```sql
SELECT ship
FROM Outcomes
WHERE battle = 'North Atlantic' AND result = 'sunk'
```
### 34

[По Вашингтонскому международному договору от начала 1922 г. запрещалось строить линейные корабли водоизмещением более 35 тыс.тонн. Укажите корабли, нарушившие этот договор (учитывать только корабли c известным годом спуска на воду). Вывести названия кораблей.](https://sql-ex.ru/learn_exercises.php?LN=34)

Решение:
```sql
SELECT name FROM classes, ships WHERE launched >=1922 AND displacement>35000 AND type='bb' AND
ships.class = classes.class
```
### 35

[В таблице Product найти модели, которые состоят только из цифр или только из латинских букв (A-Z, без учета регистра).
Вывод: номер модели, тип модели.] (https://sql-ex.ru/learn_exercises.php?LN=35)

Решение:
```sql
SELECT model, type
FROM product
WHERE upper(model) NOT like '%[^A-Z]%'
OR model not like '%[^0-9]%'
```
### 36

[Перечислите названия головных кораблей, имеющихся в базе данных (учесть корабли в Outcomes).](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT DISTINCT name as Name FROM (
SELECT name FROM ships
UNION
SELECT ship FROM outcomes
) t1
WHERE name IN (SELECT class FROM classes)
```
### 37

[Найдите классы, в которые входит только один корабль из базы данных (учесть также корабли в Outcomes).](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT c.class FROM Classes c
LEFT JOIN (Select class, name FROM Ships
UNION
SELECT Classes.class as class, Outcomes.ship as name FROM Outcomes
JOIN Classes ON Outcomes.ship = Classes.class) as s On c.class = s.class
GROUP BY c.class
HAVING COUNT(s.name)=1
```
### 38

[Найдите страны, имевшие когда-либо классы обычных боевых кораблей ('bb') и имевшие когда-либо классы крейсеров ('bc').](https://sql-ex.ru/learn_exercises.php?LN=38)

Решение:
```sql
SELECT DISTINCT country as COUNTRY
FROM classes
WHERE type='bb' AND country IN
(
SELECT country
FROM classes
WHERE type = 'bc'
)
```
### 39

[Найдите корабли, `сохранившиеся для будущих сражений`; т.е. выведенные из строя в одной битве (damaged), они участвовали в другой, произошедшей позже.](https://sql-ex.ru/learn_exercises.php#answer_ref)


Решение:
```sql
SELECT DISTINCT ship
FROM outcomes o1
LEFT JOIN Battles b1 ON b1.name = o1.battle
WHERE result = 'damaged'
and ship IN(
SELECT ship
FROM outcomes o2
LEFT JOIN Battles b2 ON b2.name = o2.battle
WHERE o2.ship=o1.ship
AND b2.date > b1.date
)
```
### 40

[Найти производителей, которые выпускают более одной модели, при этом все выпускаемые производителем модели являются продуктами одного типа.
Вывести: maker, type](https://sql-ex.ru/learn_exercises.php?LN=40)

Решение:
```sql
SELECT maker, MAX(type) as Type
FROM product
GROUP BY maker
HAVING COUNT(DISTINCT type) = 1 AND COUNT(model) > 1
```
### 41

[Для каждого производителя, у которого присутствуют модели хотя бы в одной из таблиц PC, Laptop или Printer,
определить максимальную цену на его продукцию.
Вывод: имя производителя, если среди цен на продукцию данного производителя присутствует NULL, то выводить для этого производителя NULL,
иначе максимальную цену.](https://sql-ex.ru/learn_exercises.php)

Решение:
```sql
with D as
(SELECT model, price FROM pc
UNION
SELECT model, price FROM Laptop
UNION
SELECT model, price FROM Printer)
SELECT DISTINCT P.maker,
CASE WHEN MAX(CASE WHEN D.price IS NULL THEN 1 ELSE 0 END) = 0 THEN
MAX(D.price) END
FROM Product P
RIGHT JOIN D ON P.model=D.model
GROUP BY P.maker
```
### 42

[Найдите названия кораблей, потопленных в сражениях, и название сражения, в котором они были потоплены.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT ship, battle
FROM outcomes
WHERE result='sunk'
```
### 43

[Укажите сражения, которые произошли в годы, не совпадающие ни с одним из годов спуска кораблей на воду.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT name 
FROM battles 
WHERE DATEPART(yy, date) NOT IN 
(
SELECT DATEPART(yy, date)
FROM battles
JOIN ships ON DATEPART(yy, date)=launched)
```

### 44

[Найдите названия всех кораблей в базе данных, начинающихся с буквы R.](https://sql-ex.ru/learn_exercises.php?LN=44)

Решение:
```sql
SELECT *
FROM
(
SELECT name
FROM ships
UNION
SELECT ship
FROM outcomes
) a
WHERE name LIKE 'R%'
```

### 45

[Найдите названия всех кораблей в базе данных, состоящие из трех и более слов (например, King George V).
Считать, что слова в названиях разделяются единичными пробелами, и нет концевых пробелов.](https://sql-ex.ru/learn_exercises.php?LN=45)

Решение:
```sql
SELECT *
FROM
(
SELECT name
FROM ships
UNION
SELECT ship
FROM outcomes
) a
WHERE name LIKE '% % %'
```

### 46

[Для каждого корабля, участвовавшего в сражении при Гвадалканале (Guadalcanal), вывести название, водоизмещение и число орудий.](https://sql-ex.ru/learn_exercises.php?LN=46)

Решение:
```sql
SELECT DISTINCT ship, displacement, numguns
FROM classes LEFT JOIN ships ON classes.class=ships.class RIGHT JOIN outcomes ON classes.class=ship OR ships.name=ship
WHERE battle='Guadalcanal'
```

### 47

[Определить страны, которые потеряли в сражениях все свои корабли.](https://sql-ex.ru/learn_exercises.php?LN=47)

Решение:
```sql
WITH out AS (SELECT *
FROM outcomes JOIN (SELECT ships.name s_name, classes.class s_class, classes.country s_country
FROM ships FULL JOIN classes
ON ships.class = classes.class
) u
ON outcomes.ship=u.s_class
UNION 
SELECT *
FROM outcomes JOIN (SELECT ships.name s_name, classes.class s_class, classes.country s_country
FROM ships FULL JOIN classes
ON ships.class = classes.class
) u
ON outcomes.ship=u.s_name)

SELECT fin.country
FROM (
SELECT DISTINCT t.country, COUNT(t.name) AS num_ships
FROM (
SELECT DISTINCT c.country, s.name
FROM classes c
INNER JOIN Ships s ON s.class= c.class
UNION
SELECT DISTINCT c.country, o.ship
FROM classes c
INNER JOIN Outcomes o ON o.ship= c.class) t
GROUP BY t.country

INTERSECT

SELECT out.s_country, COUNT(out.ship) AS num_ships
FROM out
WHERE out.result='sunk'
GROUP BY out.s_country) fin
```
### 48

[Найдите классы кораблей, в которых хотя бы один корабль был потоплен в сражении.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT class
FROM classes t1 LEFT JOIN outcomes t2 ON t1.class=t2.ship WHERE result='sunk'
UNION
SELECT class
FROM ships LEFT JOIN outcomes ON ships.name=outcomes.ship WHERE result='sunk'
```

### 49

[Найдите названия кораблей с орудиями калибра 16 дюймов (учесть корабли из таблицы Outcomes).](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT s.name 
FROM ships s 
JOIN classes c ON s.name=c.class OR s.class = c.class WHERE c.bore = 16
UNION
SELECT o.ship FROM outcomes o JOIN classes c ON o.ship=c.class WHERE c.bore = 16
```

### 50

[Найдите сражения, в которых участвовали корабли класса Kongo из таблицы Ships.](https://sql-ex.ru/learn_exercises.php?LN=50)

Решение:
```sql
SELECT DISTINCT o.battle
FROM ships s 
JOIN outcomes o ON s.name = o.ship WHERE s.class = 'kongo'
```

### 51

[Найдите названия кораблей, имеющих наибольшее число орудий среди всех имеющихся кораблей такого же водоизмещения (учесть корабли из таблицы Outcomes).](https://sql-ex.ru/learn_exercises.php?LN=51)

Решение:
```sql
SELECT NAME 
FROM
(
SELECT name as NAME, displacement, numguns 
FROM ships 
INNER JOIN classes ON ships.class = classes.class 
UNION 
SELECT ship as NAME, displacement, numguns 
FROM outcomes 
INNER JOIN classes ON outcomes.ship= classes.class) as d1 
INNER JOIN (SELECT displacement, max(numGuns) as numguns 
FROM
( 
SELECT displacement, numguns 
FROM ships 
INNER JOIN classes ON ships.class = classes.class 
UNION 
SELECT displacement, numguns 
FROM outcomes 
INNER JOIN classes ON outcomes.ship= classes.class) as f 
GROUP BY displacement) as d2 ON d1.displacement=d2.displacement AND d1.numguns =d2.numguns
```

### 52

[Определить названия всех кораблей из таблицы Ships, которые могут быть линейным японским кораблем,
имеющим число главных орудий не менее девяти, калибр орудий менее 19 дюймов и водоизмещение не более 65 тыс.тонн](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT s.name as NAME
FROM ships s 
JOIN classes c ON s.class = c.class WHERE country = 'japan' AND (numGuns >= '9' OR numGuns is null) AND (bore < '19' or bore is null) AND (displacement <= '65000' OR displacement is null) AND type='bb'
```

### 53

[Определите среднее число орудий для классов линейных кораблей. Получить результат с точностью до 2-х десятичных знаков.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT CAST(AVG(numguns*1.0) AS NUMERIC(6,2)) AS Avg_nmg 
FROM classes 
WHERE type = 'bb'
```

### 54

[С точностью до 2-х десятичных знаков определите среднее число орудий всех линейных кораблей (учесть корабли из таблицы Outcomes).](https://sql-ex.ru/learn_exercises.php?LN=54)

Решение:
```sql
SELECT CAST(AVG(numguns*1.0) AS NUMERIC(6,2)) as AVG_nmg 
FROM (SELECT ship, numguns, type FROM Outcomes 
JOIN classes ON ship = class
UNION
SELECT name, numguns, type 
FROM ships s 
JOIN classes c ON c.class = s.class) as x 
WHERE type = 'bb'
```

### 55

[Для каждого класса определите год, когда был спущен на воду первый корабль этого класса. Если год спуска на воду головного корабля неизвестен, определите минимальный год спуска на воду кораблей этого класса. Вывести: класс, год.](https://sql-ex.ru/learn_exercises.php?LN=55)

Решение:
```sql
SELECT c.class, min(s.launched) 
FROM classes c 
LEFT JOIN ships s ON c.class = s.class 
GROUP BY c.class
```

### 56

[Для каждого класса определите число кораблей этого класса, потопленных в сражениях. Вывести: класс и число потопленных кораблей.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT c.class, COUNT(s.ship)
FROM classes c
LEFT JOIN (SELECT o.ship, sh.class
FROM outcomes o
LEFT JOIN ships sh ON sh.name = o.ship
WHERE o.result = 'sunk') AS s ON s.class = c.class OR s.ship = c.class
GROUP BY c.class
```

### 57

[Для классов, имеющих потери в виде потопленных кораблей и не менее 3 кораблей в базе данных, вывести имя класса и число потопленных кораблей.](https://sql-ex.ru/learn_exercises.php?LN=57)

Решение:
```sql
SELECT class, COUNT(ship) count_sunked
FROM (SELECT name, class FROM ships
      UNION
      SELECT ship, ship FROM outcomes) t
LEFT JOIN outcomes ON name = ship AND result = 'sunk'
GROUP BY class
HAVING COUNT(ship) > 0 AND COUNT(*) > 2;
```

### 58

[Для каждого типа продукции и каждого производителя из таблицы Product c точностью до двух десятичных знаков найти процентное отношение числа моделей данного типа данного производителя к общему числу моделей этого производителя.
Вывод: maker, type, процентное отношение числа моделей данного типа к общему числу моделей производителя](https://sql-ex.ru/learn_exercises.php?LN=58)

Решение:
```sql
SELECT m, t,
CAST(100.0*cc/cc1 AS NUMERIC(5,2))
FROM
(SELECT m, t, sum(c) cc from
(SELECT DISTINCT maker m, 'PC' t, 0 c FROM product
UNION ALL
SELECT DISTINCT maker, 'Laptop', 0 FROM product
UNION ALL
SELECT DISTINCT maker, 'Printer', 0 FROM product
UNION ALL
SELECT maker, type, count(*) FROM product
GROUP BY maker, type) as tt
GROUP BY m, t) tt1
JOIN (
SELECT maker, count(*) cc1 FROM product GROUP BY maker
) tt2
```

### 59

[Посчитать остаток денежных средств на каждом пункте приема для базы данных с отчетностью не чаще одного раза в день. Вывод: пункт, остаток.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT c1, c2-
(CASE
WHEN o2 is null THEN 0
ELSE o2
END)
FROM
(SELECT point c1, sum(inc) c2 FROM income_o
GROUP BY point) as t1
LEFT JOIN
(SELECT point o1, sum(out) o2 FROM outcome_o
GROUP BY point) as t2
ON c1=o1
```

### 60

[Посчитать остаток денежных средств на начало дня 15/04/01 на каждом пункте приема для базы данных с отчетностью не чаще одного раза в день. Вывод: пункт, остаток.
Замечание. Не учитывать пункты, информации о которых нет до указанной даты.](https://sql-ex.ru/learn_exercises.php?LN=60)

Решение:
```sql
SELECT c1, c2-
(CASE
WHEN o2 is null THEN 0
ELSE o2
END)
FROM
(SELECT point c1, sum(inc) c2 FROM income_o
WHERE date<'2001-04-15'
GROUP BY point) as t1
LEFT JOIN
(SELECT point o1, sum(out) o2 FROM outcome_o
WHERE date<'2001-04-15'
GROUP BY point) as t2
ON c1=o1
```
### 61

[Посчитать остаток денежных средств на всех пунктах приема для базы данных с отчетностью не чаще одного раза в день.](https://sql-ex.ru/learn_exercises.php)

Решение:
```sql
SELECT sum(i) FROM
(SELECT point, SUM(inc) as i FROM
income_o
GROUP BY point
UNION

SELECT point, -sum(out) as i FROM
outcome_o
GROUP BY point
) as t
```

### 62

[Посчитать остаток денежных средств на всех пунктах приема на начало дня 15/04/01 для базы данных с отчетностью не чаще одного раза в день.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT
(SELECT sum(inc) FROM Income_o WHERE date<'2001-04-15')
-
(SELECT sum(out) FROM Outcome_o WHERE date<'2001-04-15')
AS remain
```

### 63

[Определить имена разных пассажиров, когда-либо летевших на одном и том же месте более одного раза.](https://sql-ex.ru/learn_exercises.php?LN=63)

Решение:
```sql
SELECT name FROM Passenger
WHERE ID_psg in
(SELECT ID_psg FROM Pass_in_trip
GROUP BY place, ID_psg
HAVING count(*)>1)
```

### 64

[Используя таблицы Income и Outcome, для каждого пункта приема определить дни, когда был приход, но не было расхода и наоборот.
Вывод: пункт, дата, тип операции (inc/out), денежная сумма за день.](https://sql-ex.ru/learn_exercises.php?LN=64)

Решение:
```sql
SELECT i1.point, i1.date, 'inc', sum(inc) FROM Income,
(SELECT point, date FROM Income
EXCEPT
SELECT Income.point, Income.date FROM Income
JOIN Outcome ON (Income.point=Outcome.point) AND
(Income.date=Outcome.date)
) AS i1
WHERE i1.point=Income.point AND i1.date=Income.date
GROUP BY i1.point, i1.date
UNION
SELECT o1.point, o1.date, 'out', sum(out) FROM Outcome,
(SELECT point, date FROM Outcome
EXCEPT
SELECT Income.point, Income.date FROM Income
JOIN Outcome ON (Income.point=Outcome.point) AND
(Income.date=Outcome.date)
) AS o1
WHERE o1.point=Outcome.point AND o1.date=Outcome.date
GROUP BY o1.point, o1.date
```

### 65

[Пронумеровать уникальные пары {maker, type} из Product, упорядочив их следующим образом:
- имя производителя (maker) по возрастанию;
- тип продукта (type) в порядке PC, Laptop, Printer.
Если некий производитель выпускает несколько типов продукции, то выводить его имя только в первой строке;
остальные строки для ЭТОГО производителя должны содержать пустую строку символов ('').](https://sql-ex.ru/learn_exercises.php?LN=65)

Решение:
```sql
SELECT row_number() over(ORDER BY maker,s),t, type FROM
(SELECT maker,type,
CASE
WHEN type='PC'
THEN 0
WHEN type='Laptop'
THEN 1
ELSE 2
END AS s,
CASE
WHEN type='Laptop' AND (maker in (SELECT maker FROM Product WHERE
type='PC'))
THEN ''
WHEN type='Printer' AND ((maker in (SELECT maker FROM Product WHERE
type='PC')) OR (maker in (SELECT maker FROM Product WHERE
type='Laptop')))
THEN ''
ELSE maker
END AS t
FROM Product
GROUP BY maker,type) AS t1
ORDER BY maker, s
```

### 66

[Для всех дней в интервале с 01/04/2003 по 07/04/2003 определить число рейсов из Rostov.
Вывод: дата, количество рейсов](https://sql-ex.ru/learn_exercises.php?LN=66)

Решение:
```sql
SELECT date, max(c) FROM
(SELECT date,count(*) AS c FROM Trip,
(SELECT trip_no,date FROM Pass_in_trip WHERE date>='2003-04-01' AND date<='2003-04-07' GROUP BY trip_no, date) AS t1
WHERE Trip.trip_no=t1.trip_no AND town_from='Rostov'
GROUP BY date
UNION ALL
SELECT '2003-04-01',0
UNION ALL
SELECT '2003-04-02',0
UNION ALL
SELECT '2003-04-03',0
UNION ALL
SELECT '2003-04-04',0
UNION ALL
SELECT '2003-04-05',0
UNION ALL
SELECT '2003-04-06',0
UNION ALL
SELECT '2003-04-07',0) AS t2
GROUP BY date
```

### 67

[Найти количество маршрутов, которые обслуживаются наибольшим числом рейсов.
Замечания.
1) A - B и B - A считать РАЗНЫМИ маршрутами.
2) Использовать только таблицу Trip](https://sql-ex.ru/learn_exercises.php?LN=67)

Решение:
```sql
SELECT count(*) FROM
(SELECT TOP 1 WITH TIES count(*) c, town_from, town_to FROM trip
GROUP BY town_from, town_to
ORDER BY c desc) as t
```

### 68

[Найти количество маршрутов, которые обслуживаются наибольшим числом рейсов.
Замечания.
1) A - B и B - A считать ОДНИМ И ТЕМ ЖЕ маршрутом.
2) Использовать только таблицу Trip](https://sql-ex.ru/learn_exercises.php?LN=68)

Решение:
```sql
SELECT count(*) as Count FROM (
SELECT TOP 1 WITH TIES sum(c) cc, c1, c2 FROM (
SELECT count(*) c, town_from c1, town_to c2 FROM trip
WHERE town_from>=town_to
GROUP BY town_from, town_to
UNION ALL
SELECT count(*) c,town_to, town_from FROM trip
WHERE town_to>town_from
GROUP BY town_from, town_to
) as t
GROUP BY c1,c2
ORDER BY cc DESC
) as tt
```

### 69

[По таблицам Income и Outcome для каждого пункта приема найти остатки денежных средств на конец каждого дня,
в который выполнялись операции по приходу и/или расходу на данном пункте.
Учесть при этом, что деньги не изымаются, а остатки/задолженность переходят на следующий день.
Вывод: пункт приема, день в формате "dd/mm/yyyy", остатки/задолженность на конец этого дня.](https://sql-ex.ru/learn_exercises.php?LN=69)

Решение:
```sql
with q as (
  SELECT
    isnull(i.point, o.point) point
    , isnull(i.date, o.date) date
    , coalesce(sum(i.inc), 0) - coalesce(sum(o.out), 0) balance
    FROM income i
    FULL JOIN outcome o
      ON i.point=o.point AND i.date=o.date AND i.code=o.code
    GROUP BY isnull(i.point, o.point), isnull(i.date, o.date)
)
 SELECT
  point
    -- 103 means format "dd/mm/yyyy"
  , convert(varchar, date, 103) day
  , sum(balance) over(partition by point order by date RANGE UNBOUNDED PRECEDING) as rem
  FROM q
ORDER BY point,date
```

### 70

[Укажите сражения, в которых участвовало по меньшей мере три корабля одной и той же страны.](https://sql-ex.ru/learn_exercises.php?LN=70)

Решение:
```sql
SELECT DISTINCT o.battle
FROM outcomes o
LEFT JOIN ships s ON s.name = o.ship
LEFT JOIN classes c ON o.ship = c.class OR s.class = c.class
WHERE c.country IS NOT NULL
GROUP BY c.country, o.battle
HAVING COUNT(o.ship) >= 3
```

### 71

[Найти тех производителей ПК, все модели ПК которых имеются в таблице PC.](https://sql-ex.ru/learn_exercises.php?LN=71)

Решение:
```sql
SELECT p.maker
FROM product p
LEFT JOIN pc ON pc.model = p.model
WHERE p.type = 'PC'
GROUP BY p.maker
HAVING COUNT(p.model) = COUNT(pc.model)
```

### 72

[Среди тех, кто пользуется услугами только какой-нибудь одной компании, определить имена разных пассажиров, летавших чаще других.
Вывести: имя пассажира и число полетов.](https://sql-ex.ru/learn_exercises.php?LN=72)

Решение:
```sql
SELECT TOP 1 WITH TIES name, c3 FROM passenger
JOIN
(SELECT c1, max(c3) c3 FROM
(
SELECT pass_in_trip.ID_psg c1, Trip.ID_comp c2, count(*) c3 FROM pass_in_trip
JOIN trip ON trip.trip_no=pass_in_trip.trip_no
GROUP BY pass_in_trip.ID_psg, Trip.ID_comp
) as t
group by c1
HAVING count(*)=1) as tt
ON ID_psg=c1
ORDER BY c3 DESC
```

### 73

[Для каждой страны определить сражения, в которых не участвовали корабли данной страны.
Вывод: страна, сражение](https://sql-ex.ru/learn_exercises.php?LN=73)

Решение:
```sql
SELECT c.country, b.name
FROM Classes c, Battles b
EXCEPT
SELECT c.country, o.battle
FROM Outcomes o
LEFT JOIN ships s ON o.ship=s.name
LEFT JOIN Classes c ON o.ship=c.class OR s.class=c.class
WHERE c.country is not null
GROUP BY c.country, o.battle
```

### 74

[Вывести все классы кораблей России (Russia). Если в базе данных нет классов кораблей России, вывести классы для всех имеющихся в БД стран.
Вывод: страна, класс](https://sql-ex.ru/learn_exercises.php?LN=74)

Решение:
```sql
SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' AND EXISTS (
SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' )
UNION ALL
SELECT c.country, c.class
FROM classes c
WHERE NOT EXISTS (SELECT c.country, c.class
FROM classes c
WHERE UPPER(c.country) = 'RUSSIA' )
```

### 75

[Для тех производителей, у которых есть продукты с известной ценой хотя бы в одной из таблиц Laptop, PC, Printer найти максимальные цены на каждый из типов продукции.
Вывод: maker, максимальная цена на ноутбуки, максимальная цена на ПК, максимальная цена на принтеры.
Для отсутствующих продуктов/цен использовать NULL.](https://sql-ex.ru/learn_exercises.php?LN=75)

Решение:
```sql
SELECT shipname,launched,batname
FROM
(SELECT s.name as shipname,launched,b.name as batname,
row_number() over (partition by s.name order by "date") as num
FROM ships s,battles b
WHERE to_char("date",'yyyy')>=launched
AND launched is not null)
WHERE num = 1
UNION
(
SELECT name,launched,(SELECT name FROM battles
WHERE "date" = (SELECT MAX("date") FROM battles)) as batname
FROM ships
WHERE launched is null
)
```

### 76

[Определить время, проведенное в полетах, для пассажиров, летавших всегда на разных местах. Вывод: имя пассажира, время в минутах.](https://sql-ex.ru/learn_exercises.php?LN=76)

Решение:
```sql
with pf as(
  SELECT id_psg, count(*) as place_count
  FROM pass_in_trip
  GROUP BY id_psg, place
),
pt as(
  SELECT
    pt.id_psg, pt.trip_no
    , ps.name
    , time_out, time_in
    , CASE when time_out >= time_in
        then time_in-time_out + 1440
        else time_in-time_out
    end as time
  FROM pass_in_trip pt
  JOIN passenger ps ON ps.id_psg=pt.id_psg
  JOIN (
    SELECT
      datepart(hh, time_out)*60 + datepart(mi, time_out) time_out
      , datepart(hh, time_in)*60 + datepart(mi, time_in) time_in
      , trip_no
    FROM trip t
  ) as t ON t.trip_no=pt.trip_no
  WHERE 1=ALL(select place_count FROM pf WHERE pf.id_psg=pt.id_psg)
)
SELECT
  name, sum(time) fly_time
FROM pt
GROUP BY id_psg, name
```

### 77

[Определить дни, когда было выполнено максимальное число рейсов из
Ростова ('Rostov'). Вывод: число рейсов, дата.](https://sql-ex.ru/learn_exercises.php?LN=77)

Решение:
```sql
SELECT TOP 1 WITH TIES * FROM
	(SELECT
		COUNT(distinct(pt.trip_no)) qty, pt.date
	FROM
		Trip t, Pass_in_trip pt
	WHERE t.trip_no=pt.trip_no AND t.town_from = 'Rostov'
	GROUP BY pt.date) t1
ORDER BY t1.qty DESC
```

### 78

[Для каждого сражения определить первый и последний день
месяца,
в котором оно состоялось.
Вывод: сражение, первый день месяца, последний
день месяца.

Замечание: даты представить без времени в формате "yyyy-mm-dd".](https://sql-ex.ru/learn_exercises.php?LN=78)

Решение:
```sql
SELECT name, 
REPLACE(CONVERT(CHAR(12), 
DATEADD(m, DATEDIFF(m,0,date),0), 102),'.','-') AS first_day,
             REPLACE(CONVERT(CHAR(12), DATEADD(s,-1,DATEADD(m, DATEDIFF(m,0,date)+1,0)), 102),'.','-') AS last_day
FROM Battles
```

### 79

[Определить пассажиров, которые больше других времени провели в полетах.
Вывод: имя пассажира, общее время в минутах, проведенное в полетах](https://sql-ex.ru/learn_exercises.php?LN=79)

Решение:
```sql
SELECT Passenger.name, A.minutes
FROM (SELECT P.ID_psg,
      SUM((DATEDIFF(minute, time_out, time_in) + 1440)%1440) AS minutes,
      MAX(SUM((DATEDIFF(minute, time_out, time_in) + 1440)%1440)) OVER() AS MaxMinutes
      FROM Pass_in_trip P JOIN
       Trip AS T ON P.trip_no = T.trip_no
      GROUP BY P.ID_psg
      ) AS A JOIN
 Passenger ON Passenger.ID_psg = A.ID_psg
WHERE A.minutes = A.MaxMinutes
```

### 80

[Найти производителей любой компьютерной техники, у которых нет моделей ПК, не представленных в таблице PC.](https://sql-ex.ru/learn_exercises.php?LN=80)

Решение:
```sql
SELECT DISTINCT maker
FROM product
WHERE maker NOT IN (
SELECT maker
FROM product
WHERE type='PC' AND model NOT IN (
SELECT model
FROM PC));
```
  

