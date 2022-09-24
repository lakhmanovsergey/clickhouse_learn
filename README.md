# clickhouse_learn
### Порядок запуска
1. Собираем `docker-compose build`
2. Запускаем собранные контейнеры `docker-compose ud -d`
3. Читать из базы можно WEB интерфейс `echo 'SELECT * FROM test_t' | curl 'http://localhost:8123/' --data-binary @-`
