### Домашнее задание к занятию «SQL. Часть 2» - Корольков Денис

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

Ответ:

Для выполнения этого задания мне понадобятся:
```
staff  first_name, last_name, store
address  city
customer   количество sum(customer) в каждом магазине (store)
…делаем…
```
```
SELECT CONCAT (s.first_name, ‘ ’, s.last_name) AS employee, s.store_id AS store, c1.city, COUNT(c.store_id) AS sum_customers
FROM staff
INNER JOIN address a ON a.address_id = s.address_id
INNER JOIN city c1 ON a.city_id = c1.city_id
INNER JOIN customer c ON s.store_id = c.store_id
GROUP BY s.first_name, s.last_name, s.store_id, c1.city
HAVING COUNT(c.store_id) > 300;
```

![screen1](https://github.com/KorolkovDenis/12.4-SQL-p2/blob/main/screenshots/screen1.jpg)


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

Ответ:

```
SELECT COUNT(film_id)
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```

![screen2](https://github.com/KorolkovDenis/12.4-SQL-p2/blob/main/screenshots/screen2.jpg)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

Ответ:

```
SELECT MONTH(payment_date), COUNT(payment_id), SUM(amount)
FROM payment
GROUP BY MONTH(payment_date)
ORDER BY SUM(amount) DESC
LIMIT 1;
```

![screen3](https://github.com/KorolkovDenis/12.4-SQL-p2/blob/main/screenshots/screen3.jpg)

### Были попытки сделать с подзапросом, но увы…

![screen4](https://github.com/KorolkovDenis/12.4-SQL-p2/blob/main/screenshots/screen4.jpg)
![screen5](https://github.com/KorolkovDenis/12.4-SQL-p2/blob/main/screenshots/screen5.jpg)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
