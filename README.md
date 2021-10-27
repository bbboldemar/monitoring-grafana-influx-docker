  1. "docker-compose up" поднимает на локалхосте стек из Grafana + InfluxDB, монтирует между ними сеть, дает volume и открывает порты.
  2. Настраиваем InfluxDB: создаем bucket, organization, token.
  3. telegraf запускается на машине, которой нужен мониторинг, и посылает на открытый в локалхосте порт данные. Нужно указать: bucket, organization, token, urls.
  4. Настраиваем Grafana Data source -> InfluxDB: URL (дефолт http://172.18.0.1:8086,  можно глянуть "docker network ls" -> docker inspect <NETWORK ID>), Database, HTTP      Method, Custom HTTP Headers {Header: Authorization, Value: Token <token>}
  5. Но Grafana не видит базу данных при рабочем коннекте - ее нужно смапить: открываем в cli контейнера influxdb, вставляем(правая кнопка мыши):
influx v1 dbrp create -o <organization> -t <token>\
  --db LocalHost \
  --rp LocalHost \
  --bucket-id <bucket-id> \
  --default
  6. Вы великолепны!
