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
&ensp;&ensp;Таким образом получены слудующие сервера:
- inetRouter
- centralRouter
- office1Router
- office2Router
- office1Server
- office2Server

   

  




