## Docker basics

### Мониторинг всего, чего у тебя там запущено и/или было запущено

 `docker ps -a`

### Создание контейнера

`docker run -it --name ruby -v $HOME/code:$PWD bibendi/ruby bash`
`docker run --name pg -d bibendi/pg`

### Запуск контейнера

`docker start -ai ruby`

### Запуск в запущенном контейнере еще одного процесса

`docker exec -it ruby bash`
`docker exec -it pg psql -U postgres`

### Удаление контейнера

`docker rm ruby`

### Дамп и восстановление базы ПГ

`pg_dump -Fc --no-owner --dbname=#{db_name} > #{dump_path}`
`pg_restore --clean --no-owner --dbname=#{db_name} #{dump_path}`

## Docker Compose

`docker-compose run --rm ruby`

При первом запуске нужно проставить права. Пока не смог разобраться почему так происходит

`sudo chown worker:worker /home/worker`

## Tips & Tricks

### Быстрый запуск в контейнере

Прописать такой вот alias в ~/.bashrc

```
alias d=docker-compose run --rm
alias dr=d ruby
```
