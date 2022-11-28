# my-exercises
SQL

№1: Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
Ссылка:https://sql-ex.ru/learn_exercises.php?LN=1

Решение: SELECT model, speed, hd FROM PC WHERE price < 500

№2: Найдите производителей принтеров. Вывести: maker
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=2

Решение: SELECT maker FROM Product WHERE type = 'Printer'GROUP BY maker

№3: Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.
Ссылка: https://sql-ex.ru/learn_exercises.php?LN=3

Решение: SELECT model,ram,screen FROM Laptop WHERE price > 1000

№4
