# Результат:
![image](https://github.com/Ntetikova/Docker/assets/121807872/58a9776d-8f10-4858-8602-ba093f4207c3)

# Домашнее задание к занятию «3.1. Docker»

**Важно**: прежде чем приступать, обязательно прочитайте [руководство по установке Docker](https://github.com/netology-code/aqa-homeworks/blob/master/docker/installation.md).
### Plugin IDEA

Этот раздел позволяет вам облегчить себе взаимодействие с Docker и Docker compose на первое время, воспользовавшись графическим интерфейсом.

Откройте IntelliJ IDEA, перейдите в раздел настроек:
* Windows/Linux: File -> Settings
* MacOS: IntelliJ IDEA -> Preferences

Найдите в поиске раздел Plugins:

![image](https://github.com/Ntetikova/Docker/assets/121807872/20736607-be35-4a12-863f-5eaa1e232dac)

Нажмите на кнопку `Install`, после установки перезапустите IDEA.

Теперь при открытии файлов `Dockerfile`, `docker-compose.yml` IDEA будет предлагать автодополнение и возможность запуска прямо из окна редактора:

![image](https://github.com/Ntetikova/Docker/assets/121807872/dd4d45ab-6490-4772-95d9-2df952d01bf3)

![image](https://github.com/Ntetikova/Docker/assets/121807872/8fe381d4-9b71-4305-9211-a0a65b464145)

После запуска откроется окно `Services`, где вы можете посмотреть образы, контейнеры и запущенные с помощью Docker compose сервисы:

![image](https://github.com/Ntetikova/Docker/assets/121807872/dbb3c868-7387-4b54-a72b-fee41e6b20dd)

## Задача №1: PostgreSQL

Вам необходимо подготовить приложение к тестированию на СУБД PostgreSQL. Используйте образ 12-alpine, если он недоступен, то берите последний опубликованный на Docker Hub. Возьмите собранный JAR-файл `db-api.jar`, аналогично примеру на лекции положите рядом файл `application.properties`, но в строке:
`jdbc:mysql://...` поменяйте `mysql` на `postgresql`.

Вам нужно дописать остальные настройки: хост, порт, БД, имя пользователя и пароль.

Кроме того, вам нужно подготовить файл `docker-compose.yml`, в котором прописать настройки для запуска контейнера PostgreSQL. Всю информацию о его запуске вы найдёте на официальной странице образа на Docker Hub.

Запустите сначала `docker-compose up` и только после того, как БД запустится, запустите целевое приложение: `java -jar db-api.jar`. Если нужно поменять порт запуска, по умолчанию он 9999, то добавьте в файл `application.properties` строку `server.port=<нужный номер порта>`.

Если вы сделали всё правильно, то приложение запустится и на `GET http://localhost:9999/api/cards` выдаст вам JSON с картами:
```json
[ 
   { 
      "id":1,
      "name":"Альфа-Карта Premium",
      "description":"Альфа-Карта вернёт ваши деньги",
      "imageUrl":"/alfa-card-premium.png"
   },
   { 
      "id":2,
      "name":"Alfa Travel Premium",
      "description":"Самая выгодная карта для путешествий",
      "imageUrl":"/alfa-card-travel.png"
   },
   { 
      "id":3,
      "name":"CashBack Premium",
      "description":"Заправь свою карту. Кешбэк на АЗС, в кафе и ресторанах",
      "imageUrl":"/alfa-card-cashback.png"
   }
]
```

В результате выполнения этой задачи вы должны положить в репозиторий следующие три файла (других файлов не должно быть):
* db-api.jar,
* application.properties,
* docker-compose.yml.

**Важно**: для удаления всех данных и начала с чистого листа сделайте следующее:
* `docker-compose down` в каталоге с файлом `docker-compose.yml`,
* удалите каталог для хранения данных `data`,
* запустите заново `docker-compose up`, после того как всё исправите.

**Важно**: команда `docker-compose rm` в каталоге с файлом `docker-compose.yml` удаляет сам контейнер.
