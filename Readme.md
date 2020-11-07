# Деплой приложения и инфры для поискового бота

### Краткое описание всего процесса:
 - весь проект состоит из приложения и описания инфраструктуры
 - Предполагается что сначала поднимаем инфру и дальше в ней разворачиваем наше приложение
 - Отдельная репо для разворачивания инфраструктуры в облаке: https://github.com/IsieIam/infra - следовать её инструкциям.
 - доработанные приложения(добавлены dockerfile для сборки):

https://github.com/IsieIam/search_engine_crawler

https://github.com/IsieIam/search_engine_ui

 - Оригинальное приложение:

https://github.com/express42/search_engine_crawler

https://github.com/express42/search_engine_ui

### Структура репа:
- Local - ручной локальный стенд, основанный на docker-compose (см в каталоге подробное описание)
- k8s - первичный набор yml для k8s (cм в каталого подробное описание)
- charts - Helm чарты для деплоя приложения - именно они используются для автоматичческого развертывания
- Jenkinsfile - Центральный пайплайн дженка для деплоя всего релиза в k8s

### Автоматическая сборка:

 - В доработанных репах находится Jenkins файл для сборки приложения и отправки образа в артефактори
 - После разворачивания инфраструктуры, необходимо по полученным реквизитам Jenkins создать в нем 3 job.
 - Первый job который ведет на scm источник с Jenkinsfile этого репа.
 - Два других ведут на репы сервисов crawler и ui поискового движка.
 - Для репо сервисов настраивается хук с гитхаба на адрес jenkins вида https://jenkinsip:8080/github-webhook/ (есть тонкость - дженк начнет видеть хуки только после первого ручного запуска джоба - ему нужно прочитать реп/scm)
 - В пайплайнах сервисов в postbiuld action вызывается джоб общего деплоя(в идеале надо добавить gitversion и передачу параметра версии, а также ее динамическую модификацию в helm-чарте).
 - Есть ручник - т.к. сборка приложений - это независящая от разворачивания инфраструктуры часть(на одной инфре может крутить много сервисов), то в Jenkinsfile и values.yml search-engine чарта необходимо указывать домен приложения вручную(а именно проставлять внешний ip кластера, лепить костыли на это точно не хочется :)).

###  для ручной сборки и отправки в репо можно использовать следующие команды:
```
docker build -t isieiam/se_crawler:1.0 .
docker build -t isieiam/se_ui:1.0 .

docker push isieiam/se_crawler:1.0
docker push isieiam/se_ui:1.0
```

### Проверка

Для проверки запуска сервисов можно использовать:

- тест: https://search-engine-test.ipaddress.nip.io
- прод: https://search-engine-prod.ipaddress.nip.io

### TODO
 - добавить полноценные secret
