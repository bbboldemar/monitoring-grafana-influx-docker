1. yaml поднимает на локалхосте стек из Grafana + InfluxDB, монтирует между ними сеть, дает volume и открывает порты.
2. Настраивается InfluxDB: создается bucket, organization, token.
3. telegraf запускается на машине, которой нужен мониторинг, и посылает на открытый в локалхосте порт данные. Нужно указать: bucket, organization, token, urls.
3.
