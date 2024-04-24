### Домашнее задание к занятию «ELK» - Новиков Илья

---

### Задание 1. Elasticsearch 

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.
![image](https://github.com/Dendroit/hometasks/assets/155379046/32a8bcbc-ee2c-4237-a28d-9249bb8ddeef)


---

### Задание 2. Kibana

Установите и запустите Kibana.

*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.
![image](https://github.com/Dendroit/hometasks/assets/155379046/9c16ea91-9c84-4ae2-b964-79bbfec4a09b)


---

### Задание 3. Logstash

Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.*
![image](https://github.com/Dendroit/hometasks/assets/155379046/0b178f93-573f-4971-be91-0d054fe6cc7e)


---

### Задание 4. Filebeat. 

Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.*
![image](https://github.com/Dendroit/hometasks/assets/155379046/22a98d95-0610-4db1-a2ca-c3d201aa03ce)

 
