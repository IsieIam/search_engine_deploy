# Ручной локальный стенд для YC - для быстрых тестов

## Создание машинки, проверяем что у нас есть ключик в пути --ssh-key
```
yc compute instance create \
  --name docker-host \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --memory 4 \
  --ssh-key ~/.ssh/appuser.pub
```

## Создание docker-machine, ip берем из команды выше в nat-to-nat поле
```
docker-machine create \
  --driver generic \
  --generic-ip-address=84.201.158.12 \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/appuser \
  docker-host
```
Переключение локального контекста докера на удаленную машинку
```
eval $(docker-machine env docker-host)
```
# Удаление всего
```
docker-machine rm docker-host
yc compute instance delete docker-host
```
