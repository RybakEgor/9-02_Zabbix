# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Рыбак Егор`




---

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
3. Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server

#### Требования к результаты 
1. Прикрепите в файл README.md скриншот авторизации в админке
2. Приложите в файл README.md текст использованных команд в GitHub

### Ответ:
1.
![zabbix_adm](https://github.com/RybakEgor/9-02_Zabbix/blob/main/img/zabbix_adm.png)

2.  
- wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
- dpkg -i zabbix-release_6.4-1+debian11_all.deb
- apt update
- apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
- sudo -u postgres createuser --pwprompt zabbix
- sudo -u postgres createdb -O zabbix zabbix
- zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
- nano /etc/zabbix/zabbix_server.conf
- systemctl restart zabbix-server zabbix-agent apache2
- systemctl enable zabbix-server zabbix-agent apache2
---


### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
5. Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

#### Требования к результаты 
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

### Ответ:
1. 
![zabbix_adm](https://github.com/RybakEgor/9-02_Zabbix/blob/main/img/hosts.png)
2. 
![zabbix_adm](https://github.com/RybakEgor/9-02_Zabbix/blob/main/img/working_agent_on_server.png)
3.
 ![zabbix_adm](https://github.com/RybakEgor/9-02_Zabbix/blob/main/img/latest_data.png)
4.
- wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
- dpkg -i zabbix-release_6.4-1+debian11_all.deb
- apt update
- apt install zabbix-agent
- systemctl restart zabbix-agent
- systemctl enable zabbix-agent
- sed -i 's/Server=127.0.0.1/Server=10.0.2.20'/g' /etc/zabbix/zabbix_server.conf
- systemctl restart zabbix-agent.service
- systemctl status zabbix-agent.service
---
## Задание 3 со звёздочкой*
Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

#### Требования к результаты 
1. Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:
--- 

## Критерии оценки

1. Выполнено минимум 2 обязательных задания
2. Прикреплены требуемые скриншоты и тексты 
3. Задание оформлено в шаблоне с решением и опубликовано на GitHub
