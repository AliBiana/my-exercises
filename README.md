# my-exercises
SQL - список задач:

+ [1 задание](#1)
+ [2 задание](#2)

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

№11: Найдите среднюю скорость ПК.
Cсылка: https://sql-ex.ru/learn_exercises.php?LN=11

Решение: SELECT AVG(speed) AS Avg_speed FROM pc

№12: Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
Cсылка: https://sql-ex.ru/learn_exercises.php?LN=12

Решение: SELECT AVG(speed) AS Avg_speed FROM laptop WHERE price > 1000

№13: Найдите среднюю скорость ПК, выпущенных производителем A.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=13

SELECT DISTINCT AVG(pc.speed) AS Avg_speed FROM pc JOIN product on pc.model = product.model WHERE maker = 'A'

№14: 
Решение: SELECT s.class, s.name, c.country
FROM ships s
JOIN classes c ON s.class = c.class
WHERE c.numGuns >= 10

№15:
Решение: 
SELECT hd FROM pc GROUP BY (hd) HAVING COUNT(model) >= 2

№16: 
Решение:
SELECT DISTINCT p1.model, p2.model, p1.speed, p1.ram
FROM pc p1, pc p2
WHERE p1.speed = p2.speed AND p1.ram = p2.ram AND p1.model > p2.model

№17:
Решение:
SELECT DISTINCT product.type, laptop.model, laptop.speed
FROM laptop, product
WHERE speed < (SELECT MIN(speed) FROM pc)
AND product.type ='Laptop'

№18: 
Решение: 
SELECT DISTINCT maker, price FROM product JOIN printer ON printer.model = product.model WHERE price = (SELECT MIN(price) FROM printer
WHERE color='y')
AND color='y'

№:19:
РЕШЕНИЕ: SELECT maker, AVG(screen)
FROM product JOIN laptop ON product.model=laptop.model
GROUP BY maker

№20: 
Решение: SELECT maker as Maker, COUNT(model) as Count_Model
FROM product
WHERE type='pc'
GROUP BY maker
HAVING COUNT(model)>=3

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
###29

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
