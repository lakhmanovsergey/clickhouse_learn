# clickhouse_learn
### Порядок запуска
1. Собираем `docker-compose build`
2. Запускаем собранные контейнеры `docker-compose ud -d`
3. Читать из базы можно WEB интерфейс `echo 'SELECT * FROM test_t' | curl 'http://localhost:8123/' --data-binary @-`
### ToDo
1. [] Сделать мониторинг
2. [] Оптимизировать образа
### Замечания по задаче
1. Каким образом может быть `ask_01 + bid_01 < 1`если bid в принципе не может быть < 100
