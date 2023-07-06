SQL. Часть 1. Васёв А.В.

## Задание 1
### Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```java
SELECT DISTINCT district
FROM sakila.address
where district LIKE "K%a" AND district NOT LIKE "% %";
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_1.png)

## Задание 2
### Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```java
SELECT payment_date, amount
FROM sakila.payment
WHERE CAST(payment_date AS DATE) >= "2005-06-15" AND CAST(payment_date AS DATE) <= "2005-06-18" AND amount > "10.00";
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_2.png)

## Задание 3
### Получите последние пять аренд фильмов.

```java
SELECT rental_date
FROM sakila.rental
ORDER BY rental_date DESC 
LIMIT 5;
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_3.png)

## Задание 4
### Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

    * все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
    * замените буквы 'll' в именах на 'pp'.

```java
SELECT LOWER(REPLACE(first_name, 'LL', 'PP')), LOWER(last_name), active
FROM sakila.customer
WHERE active = "1" AND first_name LIKE "Kelly" OR first_name LIKE "Willie";
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_4.png)

## Задание 5
### Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

```java
SELECT SUBSTRING_INDEX(email, '@', '1'), SUBSTRING_INDEX(email, '@', '-1')
FROM sakila.customer;
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_5.png)

## Задание 6
### Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

```java
SELECT CONCAT(LEFT(email,1),LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', '1'),2))), SUBSTRING_INDEX(email, '@', '-1')
FROM sakila.customer;
```

![alt text](https://github.com/rus42/SQL.Part1/blob/main/Task_6.png)
