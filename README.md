# Machine-learning-practice-3.8.

=============================================================================================
1 Напишите запросы к базе данных.
	а Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price.
	
SELECT model, price
FROM printer
WHERE price =
	(SELECT MAX(price)
FROM printer);

	b Найдите среднюю скорость ПК.

SELECT AVG(speed) FROM PC;

	c Найдите производителя, продающего ПК, но не ноутбуки.

SELECT AVG(speed) FROM PC;

2 Загрязните специально датасет (вставьте новые значения с уникальным кодом, но всеми остальными дублирующими полями).

insert into PC values(6,'1233',750,128,20,'50x','950');

insert into Laptop values(7,'1750',750,128,12,'1200',14);

insert into Printer values(7,'1401','n','Matrix','150');

3 Напишите оконную функцию, которая поможет вам обнаружить эти строки-редиски.

SELECT *
	from (
		select price,
			ROW_NUMBER() OVER(PARTITION BY price, model ORDER BY price desc) AS rn
	FROM pc
)q1
WHERE q1.rn > 1;

4 Обновите название колонки в таблице printer с color на color_type и поменяйте тип поля.

ALTER TABLE printer RENAME COLUMN color TO color_type

ALTER TABLE printer ALTER COLUMN color_type TYPE varchar(25);

5 В последнем пункте выполните слияние двух запросов из таблиц PC и Laptop, выбрав только те значения, у которых цена больше 500, 
а ram = 64.

SELECT ram, price, 'PC' as type
FROM PC
WHERE price > 500 AND ram = 64
union 
SELECT ram, price, 'Laptop' as type
FROM Laptop
WHERE price > 500 AND ram = 64;
