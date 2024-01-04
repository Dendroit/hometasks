###  Домашнее задание к занятию «Подъём инфраструктуры в Yandex Cloud»

---

### Задание 1 

**Выполните действия, приложите скриншот скриптов, скриншот выполненного проекта.**

От заказчика получено задание: при помощи Terraform и Ansible собрать виртуальную инфраструктуру и развернуть на ней веб-ресурс. 

В инфраструктуре нужна одна машина с ПО ОС Linux, двумя ядрами и двумя гигабайтами оперативной памяти. 

Требуется установить nginx, залить при помощи Ansible конфигурационные файлы nginx и веб-ресурса. 

Секретный токен от yandex cloud должен вводится в консоли при каждом запуске terraform.

Для выполнения этого задания нужно сгенирировать SSH-ключ командой ssh-kengen. Добавить в конфигурацию Terraform ключ в поле:

```
 metadata = {
    user-data = "${file("./meta.txt")}"
  }
``` 

В файле meta прописать: 
 
```
 users:
  - name: user
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa  xxx
```
Где xxx — это ключ из файла /home/"name_ user"/.ssh/id_rsa.pub. Примерная конфигурация Terraform:

```
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

variable "yandex_cloud_token" {
  type = string
  description = "Данная переменная потребует ввести секретный токен в консоли при запуске terraform plan/apply"
}

provider "yandex" {
  token     = var.yandex_cloud_token #секретные данные должны быть в сохранности!! Никогда не выкладывайте токен в публичный доступ.
  cloud_id  = "xxx"
  folder_id = "xxx"
  zone      = "ru-central1-a"
}

resource "yandex_compute_instance" "vm-1" {
  name = "terraform1"

  resources {
    cores  = 2
    memory = 2
  }

  boot_disk {
    initialize_params {
      image_id = "fd87kbts7j40q5b9rpjr"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }
  
  metadata = {
    user-data = "${file("./meta.txt")}"
  }

}
resource "yandex_vpc_network" "network-1" {
  name = "network1"
}

resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-b"
  network_id     = yandex_vpc_network.network-1.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

output "internal_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.ip_address
}
output "external_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.nat_ip_address
}
```

В конфигурации Ansible указать:

* внешний IP-адрес машины, полученный из output external_ ip_ address_ vm_1, в файле hosts;
* доступ в файле plabook *yml поля hosts.

```
- hosts: 138.68.85.196
  remote_user: user
  tasks:
    - service:
        name: nginx
        state: started
      become: yes
      become_method: sudo
```

Провести тестирование. 

--- 
### Решение 1

Я делал по лекции и получилось так же как у лектора

виртуалка в клауде
![image](https://github.com/Dendroit/hometasks/assets/155379046/ff080cf4-d3c4-4887-aa92-57fe66e34c1c)
и данные с terraform
<img width="585" alt="image" src="https://github.com/Dendroit/hometasks/assets/155379046/62d5a47e-a01e-4a41-95c1-e1c136a29cb6">
<img width="473" alt="image" src="https://github.com/Dendroit/hometasks/assets/155379046/5c2428ce-40ba-45a5-9a12-9085e7e8284e">
<img width="476" alt="image" src="https://github.com/Dendroit/hometasks/assets/155379046/2ac60a7d-a45b-4b89-b631-5efc7c85e765">
и в конце мы видим айпишник виртуалки. Я так же прописал ssh в cfg ansible чтобы не спрашивал

файл main.tf - (затёр персональные id'шники)
```
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

provider "yandex" {
  token     = "xxx" 
  cloud_id  = "xxx"
  folder_id = "xxx"
  zone      = "ru-central1-b"
}

resource "yandex_compute_instance" "vm2" {
  name = "linux-vm"
  allow_stopping_for_update = true
  platform_id = "standard-v2"

  resources {
    core_fraction = 100
    cores  = 2
    memory = 2 
  }

  boot_disk {
    initialize_params {
      image_id = "fd86ti70fav6g2o968vr"
    }
  }

  network_interface {
    subnet_id = "${yandex_vpc_subnet.subnet-1.id}"
    nat       = true
  }
scheduling_policy {
       preemptible = true
   }
  metadata = {
    user-data = file("./meta.yml")
  }

}
resource "yandex_vpc_network" "network-1" {
  name = "network1"
}

resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-b"
  network_id     = yandex_vpc_network.network-1.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

```
файл output.tf всего с одной ВМ т.к. не требовалось больше

```
output "ip-vm2-local" {
value = yandex_compute_instance.vm2.network_interface.0.ip_address
}
output "ip-vm2-nat" { 
value = yandex_compute_instance.vm2.network_interface.0.nat_ip_address
}

```

host.yml
для работы с nginx через ansible

```
- hosts: 158.160.8.152
  remote_user: admin
  tasks:
    - service:
        name: nginx
        state: started
      become: yes
      become_method: sudo
```
<img width="994" alt="image" src="https://github.com/Dendroit/hometasks/assets/155379046/4327b6ff-0cea-4e08-a483-21ecae21ab27">

![image](https://github.com/Dendroit/hometasks/assets/155379046/e11c6e62-9729-4dde-b73e-ee01e02521b0)

meta.yml
только затёр ssh ключ
```
 #cloud-config
 users:
  - name: admin
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa  xxx
```

--- 
