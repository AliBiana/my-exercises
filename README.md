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

№3: Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=3

Решение: SELECT model,ram,screen FROM Laptop WHERE price > 1000

№4: Найдите все записи таблицы Printer для цветных принтеров.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=4

Решение: SELECT * FROM Printer WHERE color = 'y'

№5: Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=5

Решение: SELECT model, speed, hd FROM PC WHERE ( cd = '12x' OR cd = '24x' ) AND price < 600

№6: Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=6

Решение: SELECT DISTINCT maker, speed FROM laptop JOIN 
(SELECT * FROM product WHERE type='laptop')
this_table_1 ON laptop.model = this_table_1.model
WHERE hd >= 10

№7: Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=7

Решение: SELECT DISTINCT pc.model, price FROM pc JOIN product on pc.model = product.model WHERE maker = 'B'
UNION 
SELECT DISTINCT laptop.model, price FROM laptop JOIN product on laptop.model = product.model WHERE maker = 'B'
UNION
SELECT DISTINCT printer.model, price FROM printer JOIN product on printer.model = product.model WHERE maker = 'B'

№8:Найдите производителя, выпускающего ПК, но не ПК-блокноты.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=8

Решение: SELECT maker FROM product WHERE type = 'pc'
EXCEPT
SELECT maker FROM product WHERE type = 'laptop'

№9: Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=9

Решение: SELECT DISTINCT product.maker FROM product JOIN pc on pc.model = product.model WHERE speed >= 450

№10: Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=10

Решение: SELECT DISTINCT model, price FROM printer
WHERE price = (SELECT MAX(price) FROM printer)

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
