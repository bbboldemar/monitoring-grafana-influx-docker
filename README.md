1. yaml поднимает на локалхосте стек из Grafana + InfluxDB, монтирует между ними сеть, дает volume и открывает порты.
2. Настраивается InfluxDB: создается bucket, organization, token.
3. telegraf запускается на машине, которой нужен мониторинг, и посылает на открытый в локалхосте порт данные. Нужно указать: bucket, organization, token, urls.
4. Настраиваем Grafana Data source -> InfluxDB: URL (дефолт http://172.18.0.1:8086,  можно глянуть "docker network ls" -> docker inspect <NETWORK ID>), Database, HTTP Method, Custom HTTP Headers (Header: Authorization, Value: Tokenпробел<token>)
5. Но Grafana не видит базу данных при рабочем коннекте, потому что ее нужно смапить: открываем в cli контейнера influxdb, постим(правая кнопка мыши):
influx v1 dbrp create -o BellIntegrator -t SWl2G24ASF97RaHFuO31b6cseTPDmMPgimLidHkqRZifRhyIU7MmUINRtOGRaeFQmCDarpCog8iWK0x8ki4Buw==\
  --db LocalHost \
  --rp LocalHost \
  --bucket-id 42442111d5a330bb \
  --default
6. Вы великолепны!
