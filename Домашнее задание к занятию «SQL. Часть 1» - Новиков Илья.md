# Домашнее задание к занятию «SQL. Часть 1» - Новиков Илья

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.
```
select distinct district Район 
from address
WHERE district LIKE 'K%a' and district not LIKE '% %'
order by district;
```
![1](https://github.com/user-attachments/assets/0e3a840a-8a4d-449a-83ef-a073260f631c)


### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.
```
select payment_date Дата, amount Сумма 
from payment
WHERE (CAST(payment_date AS DATE) BETWEEN "2005-06-15" AND "2005-06-18") and (amount > 10)
order by payment_date;
```
![2](https://github.com/user-attachments/assets/7f744ce0-699c-453d-9bea-941772f8af93)


### Задание 3

Получите последние пять аренд фильмов.
```
select rental_date "Дата аренды", inventory_id, customer_id 
from rental
order by rental_date desc
limit 5;
```
![3](https://github.com/user-attachments/assets/fdcef1a1-7d27-45c4-9d8f-93f8d72f4064)


### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.
```
select LOWER(first_name) Имя ,REPLACE(LOWER(first_name),'ll','pp'), LOWER(last_name) Фамилия, active
from customer
where (first_name = 'Kelly' or first_name = 'Willie') and active = 1
order by first_name, last_name;
```
![4](https://github.com/user-attachments/assets/313a58f8-e647-4f6f-b105-fdf7701b7e96)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.
```
select 	first_name Имя, last_name Фамилия, email, 
		substring_index(email,'@',1) Почта, substring_index(email,'@',-1) Домен
from customer
order by first_name, last_name;
```
![5](https://github.com/user-attachments/assets/8b42ce8f-89ff-44fa-adb1-94a843fd2963)


### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.
```
select 	first_name Имя, last_name Фамилия, email,
		#INSERT(LOWER(email), 1, 1, Upper(LEFT(email, 1))),
		INSERT(LOWER(substring_index(email,'@',1)), 1, 1, Upper(LEFT(substring_index(email,'@',1), 1))) Ящик,
		INSERT(LOWER(substring_index(email,'@',-1)), 1, 1, Upper(LEFT(substring_index(email,'@',-1), 1))) Домен
from customer;
```
![6](https://github.com/user-attachments/assets/208fe515-0570-4a75-8636-630a2639b3d2)
