# Деплой приложения и инфры для поискового бота

### Краткое описание всего процесса:

 - весь проект состоит из приложения и описания инфраструктуры
 - Предполагается что сначала поднимаем инфру и дальше в ней разворачиваем наше приложение
 - Оригинальное приложение:

https://github.com/express42/search_engine_crawler

https://github.com/express42/search_engine_ui

 - доработанное приложение(добавлены dockerfile для сборки):

https://github.com/IsieIam/search_engine_crawler

https://github.com/IsieIam/search_engine_ui

 - для ручной сборки и отправки в репо можно использовать следующие команды:
```
docker build -t isieiam/se_crawler:1.0 .
docker build -t isieiam/se_ui:1.0 .

docker push isieiam/se_crawler:1.0
docker push isieiam/se_ui:1.0
```
 - Отдельная репо для разворачивания инфраструктуры в облаке: https://github.com/IsieIam/infra

### Структура репа:

- Local - ручной локальный стенд, основанный на docker-compose (см в каталоге подробное описание)
- k8s - первичный набор yml для k8s (cм в каталого подробное описание)
- charts - Helm чарты для деплоя приложения
- Jenkinsfile - Центральный пайплайн дженка для деплоя всего релиза в k8s

### TODO
 - добавить полноценные secret
 - перевести на helmcharts
 - создать pipeline jenkins для билда, теста и деплоя
