
***Для сохранения данных и использования их разными контейнерами***
![[Pasted image 20240511173438.png|400]]

***Mapping тома для сохранения данных внутри Docker хоста*** 
```YAML
version: '3'
services:
	...
	mysql:
		image: mysql
		...
		volumes:
			- mysql_data:/var/lib/mysql  # подключение тома к контейнеру
volumes:
	mysql_data:  # том внутри Docker Host
```

***Пример использования контейнера в процессе разработки***
![[Pasted image 20240511173350.png|400]]
> *Файлы папки внутри контейнера, будут заменены файлами папки на Вашем компьютере*

***Mapping тома для РАЗРАБОТКИ***
```YAML
version: '3'
services:
	...
	frontend:
		build: ./frontend
			volumes:
			- /app/node_modules
			- ./frontend:/app
```
>`./frontend` *путь к папке на локальном компьютере*
>`/app` *путь к папке внутри контейнера*
>`/app/node_modules/` *путь к папке которую мы НЕ ХОТИМ перезаписывать внутри контейнера (если не указать, то этой папки НЕ БУДЕТ в контейнере, т.к. на локальном компьютере её нет, а создали мы её с помощью команды `RUN npm install` в Dockerfile)*

```YAML
FROM node:alpine

WORKDIR /app

EXPOSE 5000  # указание другим разработчикам об открытом порте

COPY package*.json .

RUN npm install

COPY . .

CMD ["npm", "run", "dev"]
```
> *На этапе создания образа МЫ УЖЕ КОПИРОВАЛИ все файлы из локальной папки в папку `app`, 
> но мы хотим продолжить разработку приложения, путем изменения файлов, и менять мы их будем на локальном компьютере -> те файлы, которые мы копировали в образ `COPY . .` будут уже не актуальны, когда изменим файлы локально, поэтому мы добавили `mapping` томов в файле `Docker-compose`*




>[!при mapping'е тома для разработки во frontend, у меня возникла проблема связанная с обновлением страницы в браузере, не работал Vite Hot Reload]
>Решение
>Добавил в конфиг `vite.config.js` добавлением:
```javascript
server: {
  watch: {
    usePolling: true,
  }
},
```
![[Pasted image 20240511201405.png]]

Если не отображаются изменения в браузере, проверить, сохраняются ли изменения в контейнере
```Shell
docker exec -it time-app-frontend-1 sh
cd src/components/
cat Time.vue

```

___

>[!Изменения в backend приложении не обновлялись через nodemon в браузере при запросе на localhost:5555 при mapping тома контейнера с локальными файлами]
>Решение
>Добавил в конфиг `package.json` в `"dev"`- `-L` перед `index.mjs`
>

Пример `package.json`
![[Pasted image 20240511225629.png]]