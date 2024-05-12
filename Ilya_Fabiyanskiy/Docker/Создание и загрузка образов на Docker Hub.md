***Создание образа из директории `cd frontend/`***

`docker build -t fabilya/time-app-frontend-dev .` 
>`.` *в конце указывает где находится Dockerfile*

***Загрузка образа на Docker Hub***

`docker login` *(ввести логин и пароль от https://hub.docker.com/)*
`docker push fabilya/time-app-frontend-dev`

Теперь мы можем создать новый `docker-compose.yml` и убрать создание контейнеров локально, а взять их из образов на Docker Hub:

Создали новый `docker-compose.pub.yml` 
```YAML
version: '3'  
  
services:  
  frontend:  
    image: fabilya/time-app-frontend-dev  
    restart: always  
    ports:  
      - '3000:3000'  
  api:    
    image: fabilya/time-app-backend-dev    
	restart: always    
	ports:    
      - '5555:5000'    
	depends_on:    
      - mysql    
	environment:  
      MYSQL_HOST: mysql  
      MYSQL_USER: root  
      MYSQL_PORT: '3306'  
      MYSQL_PASSWORD: password 
      MYSQL_DB: time_db 
  mysql:    
    image: mysql  
    restart: always    
	environment:  
      MYSQL_ROOT_PASSWORD: password    
	  MYSQL_DATABASE: time_db    
	volumes:  
      - mysql_data_pub:/var/lib/mysql   
  adminer:  
    image: adminer  
    restart: always  
    ports:  
      - '8888:8080'  
  
volumes:  
  mysql_data_pub:
```
> - Изменили название тома для БД (`mysql_data_pub`), чтобы том был пустой и данные из прошлого названия - не перезаписались
> - Убрали поля с `volumes:` в кастомных образах `frontend` и `api`

___
***Запуск сервисов с использованием публичных образов***
`docker-compose -f docker-compose.pub.yml up -d`
>`-f` указывает, какой именно docker-compose использовать для запуска
>`-d` "detached", запуск контейнера в бэкграунде

Для остановки и удаления контейнеров:
`docker-compose -f docker-compose.pub.yml down`
