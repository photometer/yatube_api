# API Yatube

Учебный проект в рамках курса Яндекс.Практикум

### Описание проекта:
API для Yatube - программный интерфейс, позволяющий работать c данными 
постов, групп, комментариев и подписок проекта Yatube. Авторизация 
происходит по JWT-токену.

Информацию о возможностях проекта можно найти по эндпоинту /redoc.

### Установка проекта (на Windows):

Клонировать репозиторий и перейти в него в командной строке:

```bash
git clone https://github.com/photometer/api_final_yatube
cd api_final_yatube
```
Не забудьте создать файл ```.env``` и добавить в него ваш ```SECRET_KEY```:
```
SECRET_KEY=Ваш_секретный_ключ
```
Cоздать и активировать виртуальное окружение:

```bash
python -m venv venv
source venv/scripts/activate
```

Установить зависимости из файла requirements.txt:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Зайти в директорию с файлом ```manage.py```:

```bash
cd yatube_api
```

Выполнить миграции:

```
python manage.py migrate
```

Запустить проект локально на ПК:

```
python manage.py runserver
```

### Примеры запросов к API:

##### 1. Работа с постами

- Получить список всех публикаций (возможно использование пользовательской 
пагинации):
```
GET /api/v1/posts/
GET /api/v1/posts/?offset=2&limit=5/
```

- Получить публикацию по id (где id=1):
```
GET /api/v1/posts/1/
```

- Добавление новой публикации ("text" - обязательное поле):
**анонимные запросы запрещены*
```
POST /api/v1/posts
{
    "text": "string",
    "image": "string",
    "group": 0
}
```

- Обновление публикации ("text" - обязательное поле) по id (где id=1):
**только для автора публикации*
```
PUT /api/v1/posts/1/
{
    "text": "string",
    "image": "string",
    "group": 0
}
```

- Частичное обновление публикации (PATCH) работает аналогично.

- Удаление публикации по id (где id=1):
**только для автора публикации*
```
DELETE /api/posts/1/
```

##### 2. Работа с комментариями
- Получение всех комментариев к публикации (где post_id=2):
```
GET /api/v1/posts/2/comments/
```

- Получение комментария к публикации по id (где post_id=2, id=1):
```
GET /api/v1/posts/2/comments/1/
```

- Добавление нового комментария ("text" - обязательное поле) к публикации 
(где post_id=2):
**анонимные запросы запрещены*
```
POST /api/v1/posts/2/comments/
{
    "text": "string"
}
```

- Обновление комментария ("text" - обязательное поле) к публикации по id 
(где post_id=2, id=1):
**только для автора публикации*
```
PUT /api/v1/posts/2/comments/1/
{
    "text": "string"
}
```

- Частичное обновление комментария (PATCH) работает аналогично.

- Удаление комментария к публикации по id (где post_id=2, id=1):
**только для автора публикации*
```
DELETE /api/v1/posts/2/comments/1/
```

##### 3. Работа с группами
- Получение списка доступных сообществ:
```
GET /api/v1/groups/
```

- Получение информации о сообществе по id (где id=1):
```
GET /api/v1/groups/1/
```

##### 4. Работа с подписками:
- Получение всех подписок пользователя, сделавшего запрос (возможен поиск по 
подпискам по параметру search):
*анонимные запросы запрещены*
```
GET /api/v1/follow/
GET /api/v1/follow/?search=admin
```

- Подписка пользователя, от имени которого сделан запрос на пользователя, 
переданного в теле запроса:
*анонимные запросы запрещены*
```
POST /api/v1/follow/
{
    "following": "string"
}
```

##### 5. Работа с токенами
- Получение JWT-токена:
```
POST /api/v1/jwt/create/
{
    "username": "string",
    "password": "string"
}
```

- Обновление JWT-токена:
```
POST /api/v1/jwt/refresh/
{
    "refresh": "string"
}
```

- Проверка JWT-токена:
```
POST /api/v1/jwt/verify/
{
    "token": "string"
}
```
