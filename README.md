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


# Домашнее задание 16
Изучена работа с сетью в docker
Описан docker-compose.yml
Подключены различные подсети
        Name                      Command             State           Ports
------------------------------------------------------------------------------------
sdomnicapus_comment_1   puma                          Up
sdomnicapus_post_1      python3 post_app.py           Up
sdomnicapus_post_db_1   docker-entrypoint.sh mongod   Up      27017/tcp
sdomnicapus_ui_1        puma                          Up      0.0.0.0:9292->9292/tcp
sd@ubuntu-devops:~/sdomnicapus_microservices/src$ docker network list
NETWORK ID          NAME                    DRIVER              SCOPE
21f5a916e06b        bridge                  bridge              local
024dd69153b9        host                    host                local
262303607dfb        none                    null                local
d09c9cb75a1f        reddit                  bridge              local
02a6e994d29f        sdomnicapus_back_net    bridge              local
870a732d9c16        sdomnicapus_front_net   bridge              local
faff2b368e7d        src_reddit              bridge              local
#Задание:
Узнайте как образуется базовое имя проекта. Можно ли его задать? Если можно то как? 
По-умолчанию имя папки.
Можно. Указать запуск с ключем -p или задать COMPOSE_PROJECT_NAME в .env
#Создайте docker-compose.override.yml
Описан docker-compose.override.yml 


# Домашнее задание 17
Создан шаблон packer
Описаны playbooks ansible для установки docker и docker-compose
Создан шаблон packer playbook для установки docker и docker-compose
Описаны шаблоны terraform

Изучена работа GitLab
Создан и добавлен runner для GitLab-CI

Изучена работа с pipeline
Изучена работа с окружениями

#Задание:
Автоматизация развёртывания GitLab
Описан playbook - ansible/gitlab-setup.yml

#Задание:
Автоматизация развёртывания GitLab Runner
Описан playbook - ansible/runner-setup.yml

#Задание:
Настройка оповещений в Slack
https://devops-team-otus.slack.com/archives/C0166QKTYE4


# Домашнее задание 18
Изучена работа Prometheus
Проработан мониторинг состояния микросервисов
Добавлены экспортеры для сбора метрик
Изучен ui-интерфейс Prometheus
Создана сборка Prometheus в Docker-образ
Собранные образы запушены в Docker-Hub
https://hub.docker.com/repository/docker/sdomnicapus

#Задание:
Добавить в Prometheus мониторинг MongoDB
Добавлен экспортер https://github.com/percona/mongodb_exporter

# Домашнее задание 19
Добавлен и изучена работа cAdvisor
Файл docker-compose разделене на 2
Добавлен и изучена работа Grafana
Изучен UI Grafana добавлен источник данных 
Установлен дашборд, описаны метрики для мониторинга приложения
Изучен процентиль, описаны метрики
Установлен alertmanager, описано оповещение в slack

#Задание
Добавьте сбор этих метрик в Prometheus docker
Изучено https://docs.docker.com/config/daemon/prometheus/
Добавлено
Добавлен дашборд "Docker Engine Metrics.json"

#Задание
Добавить сбор метрик Telegraf от InfluxDB
Изучено https://blog.nobugware.com/post/2016/telegraf_prometheus_metrics_swiss_army_knife/
Добавлено ./monitoring/telegraf
Добавлен дашборд grafana/dashboards/TELEGRAF.json

#Задание
Реализуйте автоматическое добавление источника данных
Изучено https://grafana.com/docs/grafana/latest/administration/provisioning/
Добавлено ./monitoring/grafana/provisioning/...

#Задание
Реализуйте схему с проксированием запросов от Grafana к Prometheus через Trickster
Добавлено ./monitoring/trickster
Добавлен дашборд grafana/dashboards/TRICKSTAR.json

# Домашнее задание 20
Пересобраны приложения с тегом logging.
Создан docker/docker-compose-logging.yml для EFK.
Создан Dockerfile, конфиг для fluentd, сбилжен и отправлен на dockerhub, а также добавлен в logging файл.
Добавлена настройка для post и ui для отправки логов в fluentd
Kibana: созданы index-pattern для индекса из потока fluentd, изучены логи приложения.
Добавлен фильтр по json, добавлен фильтр с парсером по явной регулярке в fluentd.
Изучены и добавлены описанные grok шаблоны в конфиг fluentd(распарсены часть полей логов сервиса ui).
Добавлен в docker-compose-logging zipkin - изучены возможности трассировки запросов.