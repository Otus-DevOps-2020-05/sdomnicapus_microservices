# sdomnicapus_microservices
sdomnicapus microservices repository
# Домашнее задание 14
Установлены и настроены docker, docker-compose, docker-machine
Изучены команды docker
Сделан commit на основе работающего контейнера.
Создан docker-host в yandex cloud с помощью docker-machine
Созданы файлы для работы, собран образ, описанный в Dockerfile\
Создан аккаунт на Docker Hub, выложен образ
#Дополнительные задания
Создан шаблон packer
Описаны playbooks ansible для установки docker и запуску контейнера
Описаны шаблоны terraform
Проверена работа

# Домашнее задание 15
Монолит разбит на 3 микросервиса
Подключен hadolint
Собраны певоначальные образы
Проверена работа

#Дополнительные задания 1
Перезаписываем переменные окружения при запуске контейнера

docker run -d --network=reddit --network-alias=new_post_db --network-alias=new_comment_db mongo:latest
docker run -d --env POST_DATABASE_HOST=new_post_db --network=reddit --network-alias=post sdomnicapus/post:1.0
docker run -d --env COMMENT_DATABASE_HOST=new_comment_db --network=reddit --network-alias=comment sdomnicapus/comment:1.0
docker run -d --env POST_SERVICE_HOST=post --env COMMENT_SERVICE_HOST=comment --network=reddit -p 9292:9292 sdomnicapus/ui:1.0
Уменьшили образ ui до 770 MB -> 448 MB

#Дополнительные задания 2
Образы с версией 3.0 собраны на основе ruby2.6-alpine с очисткой dev инструментов, что привело к значительному сокращению размера.
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
sdomnicapus/comment           3.0                 939b893372ed        5 seconds ago       83.9MB
sdomnicapus/ui                3.0                 e480d4bb5cf2        3 minutes ago       86MB
sdomnicapus/ui                2.0                 e3186266631b        5 minutes ago       448MB
sdomnicapus/ui                1.0                 f95c7a3b3c86        8 minutes ago       770MB
sdomnicapus/comment           1.0                 1d79ee8265c4        8 minutes ago       768MB
sdomnicapus/ubuntu-tmp-file   latest              706a74bc20ab        4 days ago          64.2MB
ubuntu                        16.04               fab5e942c505        3 weeks ago         126MB
ubuntu                        18.04               2eb2d388e1a2        3 weeks ago         64.2MB
ruby                          2.6-alpine          78349ac25912        7 weeks ago         50.4MB
hello-world                   latest              bf756fb1ae65        7 months ago        13.3kB
postgres                      11.5                5f1485c70c9a        10 months ago       293MB
ruby                          2.2                 6c8e6f9667b2        2 years ago         715MB


