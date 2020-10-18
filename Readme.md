# Деплой приложения и инфры для поискового бота

## Local - ручной локальный стенд (см в каталоге подробное описание)
## k8s - первичный набор yml для k8s
 - считаем что YC настроен (добавить мануал по настройке)
 - для текущего запуска, воспользоваться репом infra (https://github.com/IsieIam/infra) для создания k8s
 - запускаем, подставив имя кластера вместо otus-cluster:

```yc managed-kubernetes cluster get-credentials otus-cluster --external --force
```
 - на текущий момент создаем namespace:

```kubectl create namespace aznamespace
```

 - и дальше из корня:

```
 kubectl apply -f ./k8s/ -n aznamespace
```

TODO
 - добавить полноценные secret
 - переработать ingress под host (ибо приложение не умеет делать root path)
 - перевести на helmcharts
