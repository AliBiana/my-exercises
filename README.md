# my-exercises
SQL - список задач:

* [Задача 1](#1)
* [Задача 2](#2)
* [Задача 3](#3)
* [Задача 4](#4)
* [Задача 5](#5)
* [Задача 6](#6)
* [Задача 7](#7)
* [Задача 8](#8)
* [Задача 9](#9)
* [Задача 10](#10)
* [Задача 11](#11)
* [Задача 12](#12)
* [Задача 13](#13)
* [Задача 14](#14)
* [Задача 15](#15)
* [Задача 16](#16)
* [Задача 17](#17)
* [Задача 18](#18)
* [Задача 19](#19)
* [Задача 20](#20)
* [Задача 21](#21)
* [Задача 22](#22)
* [Задача 23](#23)
* [Задача 24](#24)
* [Задача 25](#25)
* [Задача 26](#26)
* [Задача 27](#27)
* [Задача 28](#28)
* [Задача 29](#29)
* [Задача 30](#30)
* [Задача 31](#31)
* [Задача 32](#32)
* [Задача 33](#33)
* [Задача 34](#34)
* [Задача 35](#35)
* [Задача 36](#36)
* [Задача 37](#37)
* [Задача 38](#38)
* [Задача 39](#39)
* [Задача 40](#40)
* [Задача 41](#41)
* [Задача 42](#42)
* [Задача 43](#43)
* [Задача 44](#44)
* [Задача 45](#45)
* [Задача 46](#46)
* [Задача 47](#47)
* [Задача 48](#48)
* [Задача 49](#49)
* [Задача 50](#50)
* [Задача 51](#51)
* [Задача 52](#52)
* [Задача 53](#53)
* [Задача 54](#54)
* [Задача 55](#55)
* [Задача 56](#56)
* [Задача 57](#57)
* [Задача 58](#58)
* [Задача 59](#59)
* [Задача 60](#60)
* [Задача 61](#61)
* [Задача 62](#62)
* [Задача 63](#63)
* [Задача 64](#64)
* [Задача 65](#65)
* [Задача 66](#66)
* [Задача 67](#67)
* [Задача 68](#68)
* [Задача 69](#69)
* [Задача 70](#70)
* [Задача 71](#71)
* [Задача 72](#72)
* [Задача 73](#73)
* [Задача 74](#74)
* [Задача 75](#75)
* [Задача 76](#76)
* [Задача 77](#77)
* [Задача 78](#78)
* [Задача 79](#79)
* [Задача 80](#80)
* [Задача 81](#81)
* [Задача 82](#82)
* [Задача 83](#83)
* [Задача 84](#84)
* [Задача 85](#85)
* [Задача 86](#86)
* [Задача 87](#87)
* [Задача 88](#88)
* [Задача 89](#89)
* [Задача 90](#90)
* [Задача 91](#91)
* [Задача 92](#92)
* [Задача 93](#93)
* [Задача 94](#94)
* [Задача 95](#95)
* [Задача 96](#96)
* [Задача 97](#97)
* [Задача 98](#98)
* [Задача 99](#99)
* [Задача 100](#100)

### 1 задание:  
[Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd](https://sql-ex.ru/learn_exercises.php?LN=1)

Решение: 
```sql
SELECT model, speed, hd FROM PC WHERE price < 500
```

### 2 задание:
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

### 21 задание:
[Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT maker as Maker, MAX(price) as Max_price FROM product
JOIN pc ON product.model = pc.model
GROUP BY maker
```
### 22 задание: 
[Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.](https://sql-ex.ru/learn_exercises.php#answer_ref)

Решение:
```sql
SELECT speed as Speed, AVG(price) as Price
FROM pc WHERE speed > 600
GROUP BY speed
```
