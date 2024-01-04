# Домашнее задание к занятию «Что такое DevOps. СI/СD» - Новиков Илья

---

### Задание 1

**Что нужно сделать:**

1. Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
2. Установите на машину с jenkins [golang](https://golang.org/doc/install).
3. Используя свой аккаунт на GitHub, сделайте себе форк [репозитория](https://github.com/netology-code/sdvps-materials.git). В этом же репозитории находится [дополнительный материал для выполнения ДЗ](https://github.com/netology-code/sdvps-materials/blob/main/CICD/8.2-hw.md).
3. Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта ```go test .``` и  ```docker build .```.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---

### Решение 1

<img width="943" alt="image" src="https://github.com/Dendroit/hometasks/assets/155379046/3cfa1e73-85fe-4e04-a5a7-70d634c3b65d">

![1](https://github.com/Dendroit/hometasks/assets/155379046/ab901127-0f95-4321-8699-213b5ddded33)
![2](https://github.com/Dendroit/hometasks/assets/155379046/e786a2f9-25c0-432b-832f-bca2b5ab068c)
<img width="438" alt="3" src="https://github.com/Dendroit/hometasks/assets/155379046/82962fcd-2341-4880-917e-ddf61dc1bd58">
![4](https://github.com/Dendroit/hometasks/assets/155379046/955caf15-d7b0-4cbc-b9b7-4f5834187ede)



---


### Задание 2

**Что нужно сделать:**

1. Создайте новый проект pipeline.
2. Перепишите сборку из задания 1 на declarative в виде кода.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.


---

### Решение 2

![1](https://github.com/Dendroit/hometasks/assets/155379046/c060571f-5e1b-4551-98f3-7e21e317da98)
![2](https://github.com/Dendroit/hometasks/assets/155379046/6d6480cf-d3bc-4764-9054-324a0b8d04be)
![3](https://github.com/Dendroit/hometasks/assets/155379046/2a9acdcd-2fe4-478b-98ef-4e65cb42985c)



---

### Задание 3

**Что нужно сделать:**

1. Установите на машину Nexus.
1. Создайте raw-hosted репозиторий.
1. Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
1. Загрузите файл в репозиторий с помощью jenkins.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---
## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.

---
### Решение 3

![1](https://github.com/Dendroit/hometasks/assets/155379046/aac7e305-2046-4baf-9fa8-91ca5d5c8758)
![2](https://github.com/Dendroit/hometasks/assets/155379046/f0810b01-bf7c-4e96-b51f-c00d8e2c73da)
![3](https://github.com/Dendroit/hometasks/assets/155379046/634718dc-97f5-4a4f-964b-22f1799e27bd)
![4](https://github.com/Dendroit/hometasks/assets/155379046/909983e8-3f37-4862-8279-1fc2cd11b6ae)
![5](https://github.com/Dendroit/hometasks/assets/155379046/58e037b9-9e37-4d19-90d6-ff85d1d31770)
![6](https://github.com/Dendroit/hometasks/assets/155379046/0fe3e26c-3e5a-4426-9b7c-8f176eea87a7)


---
