### Helm charts для деплоя приложения

- Основной chart search-engine
- пароль на rabbitmq пока as is - т.к. инфраструктура не живет долго
- для установки:

```
- На текущий момент создаем namespace:
kubectl create namespace aznamespace

- Обновляем зависимости:
helm dep update

- Устанавливаем:
helm upgrade --install search-engine . -f values.yaml -n aznamespace

- Проверяем:
search-engine.ingressipaddress.nip.io
при этом имя домена 4 уровня равно имени релиза helm

- Удаляем:
helm uninstall search-engine -n aznamespace
```
