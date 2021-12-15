# homework 2

## Создан проект в GCP

Project ID
`mongodb-test-project-335218`

пользователю ifti@yandex.ru дан доступ с ролью Project Editor

Настройки сети:
на данный момент в фаервол (GCP->VPC Network->Firewall) добавлен доступ по портам 30101 и 30201 (сервера mongo) только с моего внешнего ip (188.187.63.91)

## Создана виртаулка
для подключения по внешенму ip  добавлен свой публичный ssh ключ

но так же осталвена возможность доступа через gcloud
> gcloud compute ssh mongo-db-1
> passphrase  QOj3291#1m

создан пользователь под которым идет запуск mongo серверов через crontab
> login mongodb-user
> pass xpz*#4Ag--HjcQy6

## Развернуто два сервера mongo
1. 4.4.10 на порту 30101 установлен в системе
1. 5.0.4 на порту 30201 поднят через докер

доступ через mongo client:
> mongosh 34.88.131.236:30101 -u root -p 'otus$123' --authenticationDatabase admin

> mongosh 34.88.131.236:30201 -u root_docker -p 'otus$123' --authenticationDatabase admin

автозапкуск сделан через bash скрипт

**crontab -l** :
`@reboot	cd /home/mongodb-user && ./start_demon.sh`
**/start_demon.sh** :
> mongod --dbpath /home/mongodb-user/db1 --port 30101 --fork --logpath /home/mongodb-user/db1/db1.log --pidfilepath /home/mongodb-user/db1/db1.pid --bind_ip_all --auth

> docker start mongo-server

поднятие докер контейнера
> docker run --name mongo-server --network mongo-net -d -p 27017:30201 -v /home/mongodb-user/db2:/data/db mongo:5.0.4

## Подключится через compass не удалось
строки подключения
> mongodb://root:otus$123@34.88.131.236:30101/admin

> mongodb://root_docker:otus$123@34.88.131.236:30201/admin

compass ERROR:
`Server selection timed out after 30000 ms`


mongo server logs /home/mongodb-user/db1/db1.log :

`{"t":{"$date":"2021-12-15T21:13:01.199+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"188.187.63.91:42838","connectionId":15,"connectionCount":3}}`

`{"t":{"$date":"2021-12-15T21:13:31.193+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn15","msg":"Connection ended","attr":{"remote":"188.187.63.91:42838","connectionId":15,"connectionCount":2}}`