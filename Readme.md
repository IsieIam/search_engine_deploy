# Деплой приложения и инфры для поискового бота

## Краткое описание всего процесса:

 - весь проект состоит из приложения и описания инфраструктуры
 - Предполагается что сначала поднимаем инфру и дальше в ней разворачиваем наше приложение
 - Оригинальное приложение:
```
https://github.com/express42/search_engine_crawler
https://github.com/express42/search_engine_ui
```
 - доработанное приложение(добавлены dockerfile для сборки):
```
https://github.com/IsieIam/search_engine_crawler
https://github.com/IsieIam/search_engine_ui
```
 - для ручной сборки и отправки в репо можно использовать следующие команды:
```
docker build -t isieiam/se_crawler:1.0 .
docker build -t isieiam/se_ui:1.0 .

docker push isieiam/se_crawler:1.0
docker push isieiam/se_ui:1.0
```
 - Отдельная репо для разворачивания инфраструктуры в облаке: https://github.com/IsieIam/infra

## Local - ручной локальный стенд, основанный на docker-compose (см в каталоге подробное описание)
## k8s - первичный набор yml для k8s
 - считаем что YC настроен (добавить мануал по настройке)
 - для текущего запуска, воспользоваться репом infra (https://github.com/IsieIam/infra) для создания k8s
 - запускаем, подставив имя кластера вместо otus-cluster:

```
yc managed-kubernetes cluster get-credentials otus-cluster --external --force
```
 - на текущий момент создаем namespace:

```
kubectl create namespace aznamespace
```

 - и дальше из корня:

```
 kubectl apply -f ./k8s/ -n aznamespace
```
 - для запуска приложения http://ui.ip.nio.io

TODO
 - добавить полноценные secret
 - перевести на helmcharts
 - создать pipeline jenkins для билда, теста и деплоя
