В процессе работы вы уже отправляли запросы к серверам — из браузера, если в ответ ожидалась HTML-страница, или из кода посредством библиотеки _requests_ (когда ответ сервера надо было обработать в коде).

Для отправки запросов есть и специальные программы, заточенные под работу с API.

Такие программы можно условно разделить на консольные (такие как **curl** и **httpie**), встраиваемые (плагины для браузера или для редактора кода, например, **REST Client** для VS Code) и графические (**Postman**).

-   В **консольных** инструментах управление запросами происходит через командную строку со всеми особенностями этого подхода.
-   **Встраиваемые** инструменты — это дополнительные модули к программам. Они предоставляют графический интерфейс для работы с запросами прямо в текущем рабочем пространстве программы, в результате разработчику не приходится переключаться между приложениями.
-   Инструменты **с собственным графическим интерфейсом** — это самостоятельные программы, настольные приложения.

При разработке и тестировании вашего API вам обязательно понадобится один из этих инструментов. Не спешите устанавливать все сразу, выберите приложение, которое вам больше понравится. В дальнейшем курсе примеры запросов и ответов будут показаны в интерфейсе Postman, но решение, в какой из программ работать, остаётся за вами.

Не пожалейте времени и внимательно рассмотрите ответы тех API, к которым будут отправляться тестовые запросы в этом уроке. Там можно увидеть много интересного: структуру разных JSON, принципы вложенности и именования объектов и полей — всё то, о чём был разговор в прошлом уроке.

## Тестирование API через httpie

**httpie** — консольный API-клиент. Для знакомства с ним нет нужды его устанавливать, Попробовать его в работе можно в веб-эмуляторе. [Откройте его](https://httpie.io/run) и для активации нажмите Enter или Return.

В «веб-консоли» появится заранее написанный PUT-запрос к эндпоинту [pie.dev/put/](http://pie.dev/put/); в запросе передаётся заголовок API-Key и параметр `hello` со значением `world`.

![image](https://pictures.s3.yandex.net/resources/S09_04_01_1620135909.png)

Нажатием на Enter отправьте запрос к тестовому API — и вы увидите ответ сервера:

Скопировать кодJSON

```
PUT /put HTTP/1.1
API-Key: foo
Accept: application/json, */*;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Content-Length: 18
Content-Type: application/json
Host: pie.dev
User-Agent: HTTPie/2.3.0

{
    "hello": "world"
}

HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
CF-Cache-Status: DYNAMIC
CF-RAY: 6430db7dcc26924c-EWR
Connection: keep-alive
Content-Encoding: gzip
Content-Type: application/json
Date: Tue, 20 Apr 2021 19:42:42 GMT
NEL: {"max_age":604800,"report_to":"cf-nel"}
Report-To: {"group":"cf-nel","endpoints":[{"url":"https:\/\/a.nel.cloudflare.com\/report?s=549OJOMAtbaQ9GN45r0Ct2rFBGJcMTFRCQvUGJZ8KCIm8noJzceAWKylg6S57AlrnpJhERD6GqiKby91%2FbU1ZX%2F0HwwYXxDM"}],"max_age":604800}
Server: cloudflare
Set-Cookie: __cfduid=d5a88aa57823d025fbe244fa2bdef122b1618947762; expires=Thu, 20-May-21 19:42:42 GMT; path=/; domain=.pie.dev; HttpOnly; SameSite=Lax
Transfer-Encoding: chunked
alt-svc: h3-27=":443"; ma=86400, h3-28=":443"; ma=86400, h3-29=":443"; ma=86400
cf-request-id: 099267829e0000924c7d091000000001

{
    "args": {},
    "data": "{\"hello\": \"world\"}",
    "files": {},
    "form": {},
    "headers": {
        "Accept": "application/json, */*;q=0.5",
        "Accept-Encoding": "gzip",
        "Api-Key": "foo",
        "Cdn-Loop": "cloudflare",
        "Cf-Connecting-Ip": "192.241.133.165",
        "Cf-Ipcountry": "US",
        "Cf-Ray": "6430db7dcc26924c-FRA",
        "Cf-Request-Id": "099267829e0000924c7d091000000001",
        "Cf-Visitor": "{\"scheme\":\"http\"}",
        "Connection": "Keep-Alive",
        "Content-Length": "18",
        "Content-Type": "application/json",
        "Host": "pie.dev",
        "User-Agent": "HTTPie/2.3.0"
    },
    "json": {
        "hello": "world"
    },
    "origin": "192.241.133.165",
    "url": "http://pie.dev/put"
} 
```

Если этот консольный API-клиент придётся вам по душе — [инструкцию по установке вы найдёте там же, на сайте разработчиков](https://httpie.io/docs#installation).

## Тестирование API через расширение для VS Code

Расширение [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) позволяет прямо из VS Code отправлять HTTP-запросы и в этом же интерфейсе просматривать ответы на них. Установка расширения стандартна: в строке поиска панели “Extensions” нужно ввести название плагина “REST Client” и нажать кнопку “Install” («Установить»).

![image](https://pictures.s3.yandex.net/resources/S09_04_02_1620135986.png)

Можно потренироваться, отправляя запросы к бесплатному API проекта [{JSON} Placeholder](https://jsonplaceholder.typicode.com/). Этот проект имитирует социальную сеть: в нём хранятся посты и комментарии к ним. На главной странице проекта есть примеры запросов, описание всех доступных ресурсов, эндпоинтов и методов.

Запросы в REST Client нужно сохранять в файле с расширением .http. Если вы решите поработать с этим плагином — после установки создайте в VS Code новый файл (например requests.http) и создайте в нём запрос:

Скопировать код

```
# пример GET запроса
GET https://jsonplaceholder.typicode.com/posts/1 
```

В файле можно описать несколько разных запросов и отдельно выполнить любой из них. Запросы в файле отделяются друг от друга строками, содержащими три символа `#`.

Добавьте в файл ещё один запрос, пусть это будет POST.

POST-запросы в REST Client пишутся так:

Скопировать код

```
###

POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
    "title": "My Title",
    "body": "My text",
    "userId": 1
} 
```

Для отправки любого запроса нажмите над ним ссылку “SendRequest”. В правой части экрана вы увидите ответ сервера:

![image](https://pictures.s3.yandex.net/resources/S09_04_03_1620136055.png)

Файл с запросами можно сохранить в репозитории, и любой разработчик сможет отправить сохранённые запросы и посмотреть результат.

## Тестирование API через Postman

**Postman** — популярный и удобный API-клиент, он умеет отправлять запросы и показывать ответы, сохраняет историю запросов и данные об аутентификации, позволяет проектировать и тестировать API.

Управлять запросами в Postman можно и через браузерное приложение, но для работы с локальным проектом потребуется скачать и установить программу на компьютер: работать через браузер с локальным IP 127.0.0.1 не получится, он не будет доступен.

Скачайте Postman со [страницы загрузки](https://www.postman.com/downloads/) проекта и установите его на свою рабочую машину.

### Установка Postman

![image](https://pictures.s3.yandex.net/resources/S09_04_04_1620136059.png)

Авторизуйтесь в приложении, это позволит работать в интерфейсе **Workspace** (системе для создания и сохранения запросов для каждого проекта по отдельности) и даст некоторые другие бонусы, например — хранение настроек и истории запросов в облаке.

### Postman Workspace

Postman может сохранять запросы, ответы, токены и другую рабочую информацию; вы в любой момент можете одним кликом отправить заранее настроенный и сохранённый запрос. При работе с несколькими проектами удобно разделять эти данные, хранить данные каждого проекта отдельно.

**Workspace** — это своего рода окружение проекта, cпособ разделить настройки разных сервисов.

Например, вы тестировали сервис с котиками, установили для него токен аутентификации, сохранили примеры запросов, всё настроили — а потом вам пришлось перейти к тестированию другого проекта, с пёсиками например.

В такой ситуации Workspace в Postman позволит просто переключиться на другое окружение и создать там другие запросы и токены, относящиеся к новому проекту.

На стартовой странице приложения выберите закладку “Workspace” и нажмите на “My Workspace” — это первое, предварительно созданное рабочее окружение. Его можно переименовать и настроить в нём запросы для своего проекта.

![image](https://pictures.s3.yandex.net/resources/S09_04_05_1620136061.png)

После нажатия на кнопку “My Workspace” откроется основной интерфейс Postman.

![image](https://pictures.s3.yandex.net/resources/S09_04_06_1620136064.png)

Главный экран делится на две части:

-   слева — список сохранённых запросов и история изменений, у вас их пока нет;
-   справа — рабочая область: тут можно создавать запросы и настраивать их.

Интерфейс может немного отличаться от скриншотов — это зависит от версии программы, но функциональность остаётся та же.

Чтобы создать запрос, кликните по кнопке «**+**» над рабочей областью.

![image](https://pictures.s3.yandex.net/resources/S09_04_07_1620136067.png)

### Окно настройки запроса

Здесь можно указать и отредактировать любые настройки:

-   метод запроса;
-   URL, по которому нужно отправить запрос;
-   параметры запроса;
-   заголовки запроса;
-   тело запроса.

![image](https://pictures.s3.yandex.net/resources/S09_04_08_1_1620203596.png)

Теперь можно поупражняться.

У GitHub есть [отлично документированное API](https://docs.github.com/en/rest), вот туда и отправьте тестовый GET запрос на получение данных аккаунта _yandex-praktikum_:

Скопировать код

```
 https://api.github.com/users/yandex-praktikum 
```

Если всё сделано как надо — ответ будет таким:

Скопировать кодJSON

```
{
    "login": "yandex-praktikum",
    "id": 58176914,
    "node_id": "MDQ6VXNlcjU4MTc2OTE0",
    "avatar_url": "https://avatars.githubusercontent.com/u/58176914?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/yandex-praktikum",
    "html_url": "https://github.com/yandex-praktikum",
    "followers_url": "https://api.github.com/users/yandex-praktikum/followers",
    "following_url": "https://api.github.com/users/yandex-praktikum/following{/other_user}",
    "gists_url": "https://api.github.com/users/yandex-praktikum/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/yandex-praktikum/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/yandex-praktikum/subscriptions",
    "organizations_url": "https://api.github.com/users/yandex-praktikum/orgs",
    "repos_url": "https://api.github.com/users/yandex-praktikum/repos",
    "events_url": "https://api.github.com/users/yandex-praktikum/events{/privacy}",
    "received_events_url": "https://api.github.com/users/yandex-praktikum/received_events",
    "type": "User",
    "site_admin": false,
    "name": null,
    "company": null,
    "blog": "",
    "location": null,
    "email": null,
    "hireable": null,
    "bio": null,
    "twitter_username": null,
    "public_repos": 6,
    "public_gists": 0,
    "followers": 90,
    "following": 0,
    "created_at": "2019-11-25T13:38:59Z",
    "updated_at": "2021-03-24T16:15:56Z"
} 
```

Данные аккаунтов на Github открыты, получить их может кто угодно. Запросите данные своего аккаунта:

Скопировать код

```
https://api.github.com/users/<ваш-логин-на-гитхабе> 
```

Можно получить информацию и о конкретном репозитории в аккаунте: надо лишь [покопаться в документации](https://docs.github.com/en/rest/reference/repos#get-a-repository) и найти нужный метод.

Пора создать свой API и подёргать его запросами за усы.