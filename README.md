# Архитектура сетей
1. Скачать и развернуть Vagrant-стенд https://github.com/erlong15/otus-linux/tree/network;
2. Построить следующую сетевую архитектуру:<br/>
   Сеть office1:
   - 192.168.2.0/26   - dev
   - 192.168.2.64/26  - test servers
   - 192.168.2.128/26 - managers
   - 192.168.2.192/26 - office hardware

   Сеть office2:
   - 192.168.1.0/25   - dev
   - 192.168.1.128/26 - test servers
   - 192.168.1.192/26 - office hardware

   Сеть central:
   - 192.168.0.0/28  - directors
   - 192.168.0.32/28 - office hardware
   - 192.168.0.64/26 - wifi
     
![изображение](https://github.com/DemBeshtau/18_DZ/assets/149678567/c4704775-1c02-4086-a4df-af8ed660be66)<br/>
&ensp;&ensp;Таким образом планируется получить следующие сервера:
- inetRouter
- centralRouter
- office1Router
- office2Router
- office1Server
- office2Server
3. Реализовать теоретическую часть задания:
  - Найти свободные подсети;
  - Посчитать количество узлов в каждой подсети, включая свободные;
  - Указать broadcast-адрес для каждой подсети;
  - Проверить, нет ли ошибок при разбиении.
4. Реализовать практическую часть задания:
  - Соединить офисы в сеть согласно логической схемы и настроить маршруты;
  - Интернет-трафик со всех серверов должен проходить через inetRouter;
  - Все сервера должны видеть друг друга (должен проходить ping);
  - У всех новых серверов отключить дефолт на NAT (eth0), который Vagrant поднимает для связи;
  - Добавить дополнительные сетевые интерфейсы, если потребуется.
### Исходные данные ###
&ensp;&ensp;ПК на Linux c 8 ГБ ОЗУ или виртуальная машина (ВМ) с включенной Nested Virtualization.<br/>
&ensp;&ensp;Предварительно установленное и настроенное ПО:<br/>
&ensp;&ensp;&ensp;Hashicorp Vagrant (https://www.vagrantup.com/downloads);<br/>
&ensp;&ensp;&ensp;Oracle VirtualBox (https://www.virtualbox.org/wiki/Linux_Downloads).<br/>
&ensp;&ensp;&ensp;Ansible (https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).<br/>
&ensp;&ensp;Все действия проводились с использованием Vagrant 2.4.0, VirtualBox 7.0.18, Ansible 9.4.0 и образа ubuntu/jammy64 версии 20240301.0.0. <br/> 
### Ход решения ###
##### 1. Теоретическая часть #####
- В соответствии с условием теоретической части задания посчитаны данные по подсетям и подготовлена следующая таблица топологии сети:<br/>

![изображение](https://github.com/DemBeshtau/18_DZ/assets/149678567/b5abdfd8-43eb-4ce7-b108-dd32d6f041fc) <br/>

- Полученные данные свидетельствуют об остуствии ошибок при планировании сети, а также о наличии свободных подсетей: <br/>

![изображение](https://github.com/DemBeshtau/18_DZ/assets/149678567/d2fb69b8-681e-42da-b3df-51bafc579247) <br/>

##### 2. Практическая часть #####
- По итогам изучения таблицы топологии сети и предложенной конфигурации Vagrant, принято решение о добавлении двух сетей для соединения роутеров office1Router и office2Router с centralRouter. Для осуществления данного мероприятия задействованы 2 подсети из установленного списка свободных сетей.
Ниже представлена полная схема спроектированной сети.<br/>

![test](https://github.com/DemBeshtau/18_DZ/assets/149678567/84ccfd4a-1526-45a1-a74f-3606bb3f7bea)

- На основании схемы получен список серверов:<br/>
![изображение](https://github.com/DemBeshtau/18_DZ/assets/149678567/9b98d1cc-c922-4910-b802-e041ecbe3055)<br/>
- В соответствии со схемой в Vagrant-файл добавлены 4 новых сервера, кроме того, к старым серверам добавлены 2 дополнительных интерфейса для соединения сетей офисов.
- Настройка NAT на сервере inetRouter.
  Отключение фаервола ufw:
```shell
root@inetRouter:~# systemctl stop ufw
root@inetRouter:~# systemctl disable ufw
```
   Установка пакета iptables-persistent для автоматического восстановления правил iptables и добавление необходимых правил фильтрации и NAT:
```shell
root@inetRouter:~# apt update; apt install iptables-persistent
...
root@inetRouter:~# 
```


  

   




   

  




