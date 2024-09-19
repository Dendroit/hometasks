# Домашнее задание к занятию «SQL. Часть 2» - Новиков Илья

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.
```
select s.store_id Магазин, concat(s2.last_name, " ",s2.first_name) Продавец, c.city Город, cl Клиенты
from store s 
join staff s2 on s2.staff_id = s.manager_staff_id
join address a on a.address_id = s.address_id 
join city c on c.city_id = a.city_id
JOIN (select store_id, COUNT(store_id) as cl
	from customer
	GROUP BY store_id) cc on cc.store_id = s.store_id
WHERE cl > 300
```

![1](https://github.com/user-attachments/assets/c811d980-4302-4bb0-901b-64c9aff6a8fb)




### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
```
select count(1)  
from film f
where length > (
	select avg(length) from film
	)
```
![2](https://github.com/user-attachments/assets/a35f566d-ad15-4fcc-a9ac-8e65e6bfc524)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
```
select DATE_FORMAT(payment_date, '%m-%Y') as Месяц, SUM(amount) as Сумма, count(rental_id) as Аренды
from payment as pp
GROUP BY Месяц
having Сумма = (select max(ss) from 
(select DATE_FORMAT(payment_date, '%m-%Y') as dd, SUM(amount) as ss 
from payment
GROUP BY dd) as qss)
```
![3](https://github.com/user-attachments/assets/57146d61-b7d1-4286-8b4a-2ecc6c766ca0)
 
## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».
```
select r.staff_id st, count(1) as pr,
CASE
	WHEN count(1) > 8000 THEN 'Да'
	ELSE 'Нет'
	END AS 'Премия'
from rental r 
GROUP BY st
```
![4](https://github.com/user-attachments/assets/dfc99a64-c377-452e-a718-0c8f4aabf48d)

   
### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
```
select f.title Фильм, ar.col Аренды
from film f
left join 
	(select i.film_id, count(i.film_id) as col
	from inventory i 
	GROUP BY i.film_id) ar
	on f.film_id = ar.film_id
 where ar.col IS null;
```
![5](https://github.com/user-attachments/assets/b00885a4-6009-48aa-85da-cdf34f9afab8)
