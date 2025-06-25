# HOMEWORK_BD3_ELK_Beats



```
sudo docker compose up -d
```
Убить контейнеры без удаления томов.
```
sudo docker compose down 
```
Убить контейнеры с удалением всех  томов
```
sudo docker compose down -v
```
Ключ -v (--volumes) дополнительно удаляет тома (volumes)


Переподнять 
```
sudo docker compose down -v && sudo docker compose up -d
```

!!!Крайне не желательно!!!
```
sudo docker compose down --rmi all
```



# Задание 1. Elasticsearch
Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный.

Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name.
```
 curl -X GET 'http://localhost:9200/_cluster/health?pretty'
```


![alt text](image.png)



Задание 2. Kibana
Установите и запустите Kibana.

Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty.
```
http://192.168.31.126:5601/app/dev_tools#/console
```
![alt text](image-1.png)


Задание 3. Logstash
Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.

применим  конфиг

```
sudo docker compose down -v && sudo docker compose up -d
```
зайдем в логи logstash

```
docker logs -f homework_bd3_elk_beats-logstash-1
```
в соседней   консоли выполним
```
echo "10.40.31.120 no  31200" | nc  localhost 5000
```
![alt text](image-2.png)

проверим что обрабатываются логи nginx

в соседней   консоли выполним
```
curl http://localhost:8080

```
![alt text](image-3.png)

видим что логи обрабатываются 
![alt text](image-4.png)



Задание 4. Filebeat.
Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.
![alt text](image-5.png)


![alt text](image-6.png)

#### Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

Задание 5*. Доставка данных
Настройте поставку лога в Elasticsearch через Logstash и Filebeat любого другого сервиса , но не Nginx. Для этого лог должен писаться на файловую систему, Logstash должен корректно его распарсить и разложить на поля.

Приведите скриншот интерфейса Kibana, на котором будет виден этот лог и напишите лог какого приложения отправляется.