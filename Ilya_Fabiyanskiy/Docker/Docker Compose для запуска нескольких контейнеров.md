
Императивный подход - выполнение команд пошагово
`docker run`
`docker stop`
`docker build` и т.д.

Декларативный подход - описание желаемого результата (абстрагирование от пошаговых команд и создание инструкций высокого уровня, и с помощью инструкций описываете конечную цель)

***Пример `docker_compose.yml` файла***
```YAML
version: '3'

services:
	app:
		build: ./app
	mongo:
		image: mongo
```
>С помощью `yaml` файлов создаются инструкции для создания или скачивания образов с Docker Hub и для запуска многих контейнеров, в таком же файле могут находиться инструкции касательно [[Mapping томов|порт mapping'а]] или mapping'а томов

***Структура и формат `YAML` файлов:***

1. Списки
```YAML
fruits:
	- banana
	- apple
	- orange
```

2. Словари
```YAML
pen:
	color: yellow
	model:
		type: pen
		material: plastic
	price: 2
```

***Преимущества DOCKER COMPOSE***
- Декларативный подход к созданию контейнеров
- Все необходимые контейнеры запускаются одной командой `docker compose up`
- Автоматическое создание необходимых образов на основании Dockerfile каждого приложения
- Автоматическое создание изолированной сети для взаимодействия контейнеров
- Благодаря [[DNS (Domain name server)]] возможно взаимодействие между контейнерами, используя имена сервисов

Пример `docker-compose.yml`:
```YAML
version: '3'

services:
	app:  # Названия сервисов вы выбираете сами, Docker создаст контейнер
		build: ./app # создание образа на основе Dockerfile, который лежит в `./app`
	mongo:  # Названия сервисов вы выбираете сами, Docker создаст контейнер
		image: mongo  # mongo - название официального образа
```
>Для запуска `docker-compose up`
>Для остановки сервисов - `docker-compose down`, так же автоматически удалятся контейнеры
>Для перезаписи образов - `docker-compose up --build` 

___

Пример `docker-compose.yml` с использованием [[Mapping томов]] и портов
```YAML
version: '3'  
  
services:  
  frontend:  
    build: ./frontend  
    restart: always  
    ports:  
      - '3000:3000'  
    volumes:  
      - /app/node_modules  
      - ./frontend:/app  
  api:  
    build: ./api  
    restart: always  
    ports:  
      - '5555:5000'  
    depends_on:  
      - mysql  
    volumes:  
      - /app/node_modules  
      - ./api:/app  
  mysql:  
    image: mysql  
    restart: always  
    environment:  
      MYSQL_ROOT_PASSWORD: password  
      MYSQL_DATABASE: time_db  
    volumes:  
      - mysql_data:/var/lib/mysql  
  adminer:  
    image: adminer  
    restart: always  
    ports:  
      - '8888:8080'  
  
volumes:  
  mysql_data:
```