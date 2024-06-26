# Домашнее задание к занятию «Кеширование Redis/memcached» - Новиков Илья

---

### Задание 1. Кеширование 

Приведите примеры проблем, которые может решить кеширование.

- Увеличение скорости ответа
- Повышение производительности
- Сглаживание бустов трафика
- Оптимизация нагрузки на базы данных

---
### Задание 2. Memcached

Установите и запустите memcached.

*Приведите скриншот systemctl status memcached, где будет видно, что memcached запущен.*

выполнял через docker-compose
![image](https://github.com/Dendroit/hometasks/assets/155379046/5f01a218-35db-4d17-81e6-d8839a39ae13)

---

### Задание 3. Удаление по TTL в Memcached

Запишите в memcached несколько ключей с любыми именами и значениями, для которых выставлен TTL 5. 

*Приведите скриншот, на котором видно, что спустя 5 секунд ключи удалились из базы.*

- **Скрипт для выполнения задания на Python 3**
```
from pymemcache.client import base
import time

db = base.Client(('localhost', 11211))

db.set('a1', '100', 5)
db.set('a2', '200', 5)
db.set('a3', '300', 5)

print("a1 - ", db.get('a1'))
print("a2 - ", db.get('a2'))
print("a3 - ", db.get('a3'))

print("   Ожидание 5 секунд...")
time.sleep(5)

print("a1 - ", db.get('a1'))
print("a2 - ", db.get('a2'))
print("a3 - ", db.get('a3'))
```
![image](https://github.com/Dendroit/hometasks/assets/155379046/b0e9fa4f-2827-431f-9967-447b9069bd32)

---

### Задание 4. Запись данных в Redis

Запишите в Redis несколько ключей с любыми именами и значениями. 

*Через redis-cli достаньте все записанные ключи и значения из базы, приведите скриншот этой операции.*
![image](https://github.com/Dendroit/hometasks/assets/155379046/d110c6dd-24ff-446c-a5b2-504d0bf85a19)

---

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже разобраться в материале.

### Задание 5*. Работа с числами 

Запишите в Redis ключ key5 со значением типа "int" равным числу 5. Увеличьте его на 5, чтобы в итоге в значении лежало число 10.  

*Приведите скриншот, где будут проделаны все операции и будет видно, что значение key5 стало равно 10.*
![image](https://github.com/Dendroit/hometasks/assets/155379046/2c6ccc85-09b9-4ffc-b488-9a48e927fea3)

