Задание 1.

1.
CREATE TABLE city(
city_id BIGSERIAL NOT NULL PRIMARY KEY,
city_name VARCHAR(60)NOT NULL
);

2 и 3.
ALTER TABLE employees ADD city_id BIGINT REFERENCES city(city_id);

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

1.
SELECT first_name,last_name,city_name
FROM city
INNER JOIN employees
ON employees.city_id=city.city_id;

2.
//создан лишний город, чтобы вернул null на работниках
INSERT INTO city(
city_name)
VALUES('Волгоград');

SELECT city_name,first_name,last_name
FROM city
LEFT JOIN employees
ON employees.city_id=city.city_id;

3.
//созданы лишние имена, фамилии работников, чтобы вернул null на городах
INSERT INTO employees(
first_name,last_name,age)
VALUES('Валентин','Афанасьев', 28);
INSERT INTO employees(
first_name,last_name,age)
VALUES('Игорь','Васин', 40);

SELECT first_name,city_name
FROM city
RIGHT JOIN employees
ON employees.city_id=city.city_id;

4.
SELECT first_name,city_name
FROM city
CROSS JOIN employees;
