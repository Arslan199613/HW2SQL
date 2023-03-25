Задание 1.

1.
CREATE TABLE city(
city_id BIGSERIAL NOT NULL PRIMARY KEY,
city_name VARCHAR(60)NOT NULL
);

2 и 3.
ALTER TABLE employees ADD city_id BIGINT REFERENCES city(city_id);

либо

ALTER TABLE
employees ADD city_id INT;
ALTER TABLE
employees ADD CONSTRAINT city_id FOREIGN KEY(city_id) REFERENCE city(city_id);

4. // Заполнил таблицу city
INSERT INTO city(
city_name)
VALUES('Казань');
INSERT INTO city(
city_name)
VALUES('Москва');
INSERT INTO city(
city_name)
VALUES('Сочи');
INSERT INTO city(
city_name)
VALUES('Воронеж');

UPDATE employees SET city_id=1 WHERE id=1;
UPDATE employees SET city_id=2 WHERE id=2;
UPDATE employees SET city_id=3 WHERE id=3;
UPDATE employees SET city_id=4 WHERE id=4;
UPDATE employees SET city_id=5 WHERE id=5;

SELECT city_name,first_name
FROM city
INNER JOIN employees
ON employees.city_id=city.city_id;

Задание 2.
//Получите имена и фамилии сотрудников, а также города, в которых они проживают.

1.
SELECT first_name,last_name,city_name
FROM city
INNER JOIN employees
ON employees.city_id=city.city_id;

//Получите города, а также имена и фамилии сотрудников, которые в них проживают.
//Если в городе никто из сотрудников не живет, то вместо имени должен стоять null.
2.
SELECT first_name, last_name,city_name
FROM employee
INNER JOIN city
ON employee.city_id=city1.city_id;

//Получите имена всех сотрудников и названия всех городов. Если в городе не живет никто из сотрудников, то вместо имени должен стоять null.
//Аналогично, если города для какого-то из сотрудников нет в списке, так же должен быть получен null.
3.
SELECT first_name, last_name,city_name
FROM city
LEFT JOIN employee
ON city.city_id=employee.city_id;

//Получите таблицу, в которой каждому имени должен соответствовать каждый город.
4.
SELECT first_name, city_name
FROM employee
CROSS JOIN city;

//Получить имена городов, в которых никто не живет
5.
SELECT city_name
FROM city
LEFT JOIN employee
ON city.city_id=employee.city_id WHERE employee.first_name IS NULL;
