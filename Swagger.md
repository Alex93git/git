Создание Swagger документации для API является важным шагом, который помогает разработчикам и пользователям понимать, как взаимодействовать с вашим API. Swagger, ныне известный как OpenAPI, предоставляет формат для описания API с использованием YAML или JSON. 

В этой инструкции мы рассмотрим, как написать Swagger описание API с использованием YAML.

## Шаг 1: Установка Swagger Editor

### Вариант 1: Онлайн редактор

Вы можете использовать [Swagger Editor онлайн](https://editor.swagger.io/), чтобы написать и проверить вашу документацию.

### Вариант 2: Установка локально

1. Установите Node.js, если он ещё не установлен. Загрузите его с [официального сайта Node.js](https://nodejs.org/).
2. Установите Swagger Editor глобально:
   ```bash
   npm install -g swagger-editor
   ```
3. Запустите Swagger Editor:
   ```bash
   swagger-editor
   ```
   Swagger Editor будет доступен по адресу [http://localhost:8080](http://localhost:8080).

## Шаг 2: Начало написания документации

Создайте файл `swagger.yaml` или используйте онлайн-редактор для написания документации.

```yaml
openapi: 3.0.0
info:
  title: Sample API
  description: This is a sample API to demonstrate Swagger documentation.
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
    description: Production server
  - url: https://staging-api.example.com/v1
    description: Staging server
paths:
  /users:
    get:
      summary: Get a list of users
      description: Retrieve a list of users with their details.
      responses:
        '200':
          description: A list of users.
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
    post:
      summary: Create a new user
      requestBody:
        description: User object that needs to be added
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/NewUser'
      responses:
        '201':
          description: User created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '400':
          description: Invalid input
  /users/{id}:
    get:
      summary: Get a user by ID
      parameters:
        - name: id
          in: path
          required: true
          description: ID of user to return
          schema:
            type: integer
            format: int64
      responses:
        '200':
          description: User object
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: User not found
    put:
      summary: Update an existing user
      parameters:
        - name: id
          in: path
          required: true
          description: ID of user to update
          schema:
            type: integer
            format: int64
      requestBody:
        description: User object that needs to be updated
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UpdateUser'
      responses:
        '200':
          description: User updated successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '400':
          description: Invalid ID supplied
        '404':
          description: User not found
    delete:
      summary: Delete a user by ID
      parameters:
        - name: id
          in: path
          required: true
          description: ID of user to delete
          schema:
            type: integer
            format: int64
      responses:
        '204':
          description: User deleted successfully
        '400':
          description: Invalid ID supplied
        '404':
          description: User not found

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
          format: int64
        username:
          type: string
        email:
          type: string
    NewUser:
      type: object
      properties:
        username:
          type: string
        email:
          type: string
        password:
          type: string
      required:
        - username
        - email
        - password
    UpdateUser:
      type: object
      properties:
        username:
          type: string
        email:
          type: string
        password:
          type: string
      required:
        - username
        - email

```

### Подробное объяснение структуры

1. **openapi**: Указывает версию OpenAPI Specification. Здесь используется версия `3.0.0`.

2. **info**: Содержит метаинформацию об API, включая название, описание и версию.

3. **servers**: Описывает сервера, на которых доступен ваш API. Можно указать несколько серверов, например, для production и staging.

4. **paths**: Определяет доступные пути и операции для каждого из них.

5. **components**: Содержит определения схем, которые можно использовать в различных частях описания, например, в ответах, запросах и параметрах.

#### Описание путей

Каждый путь содержит набор операций, таких как GET, POST, PUT, DELETE и т.д. Описание каждой операции включает в себя:

- **summary**: Краткое описание операции.
- **description**: Детальное описание того, что делает операция.
- **parameters**: Параметры запроса или пути, которые операция принимает.
- **requestBody**: Описание тела запроса (только для операций POST и PUT).
- **responses**: Описывает возможные ответы, которые может вернуть операция. Для каждого кода состояния HTTP указывается описание и схема данных.

#### Описание схем

В разделе **components** можно определить схемы (schemas), которые представляют данные, используемые в вашем API. Например:

- **User**: Схема пользователя с полями `id`, `username`, `email`.
- **NewUser**: Схема для создания нового пользователя, содержит обязательные поля `username`, `email` и `password`.
- **UpdateUser**: Схема для обновления пользователя, включает опциональные поля `username`, `email`, `password`.

### Пример использования API с использованием Swagger UI

Для использования Swagger UI:

1. Перейдите на сайт [Swagger UI](https://swagger.io/tools/swagger-ui/).
2. Введите URL вашего Swagger YAML файла в поле ввода и нажмите **Explore**.
3. Вы сможете просмотреть документацию и протестировать API.

## Шаг 3: Расширенное описание (опционально)

Вы можете дополнительно добавить:

- **Security**: Описание методов аутентификации и авторизации.
- **Tags**: Категоризация путей для лучшей структуризации документации.
- **ExternalDocs**: Ссылки на внешние документы, такие как спецификации, описания и т.д.

### Пример с аутентификацией

Добавим аутентификацию с использованием JWT:

```yaml
openapi: 3.0.0
info:
  title: Sample API with Auth
  description: This API demonstrates authentication with JWT.
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
paths:
  /login:
    post:
      summary: User login
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        '200':
          description: JWT token
          content:
            application/json:
              schema:
                type: object
                properties:
                  token:
                    type: string
        '401':
          description: Unauthorized
  /secure-data:
    get:
      summary: Get secure data
      security:
        - bearerAuth: []
      responses:
        '200':
          description: Secure data
        '401':
          description: Unauthorized

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
  schemas:
    LoginRequest:
      type: object
      properties:
        username:
          type: string
        password:
          type: string
      required:
        - username
        - password
```

### Объяснение

- **securitySchemes**: Описывает методы аутентификации, используемые в API. В этом примере используется `bearerAuth` с JWT.
- **security**: Указывает, какие методы аутентификации необходимы для выполнения операций на определённых путях.

## Заключение

Теперь у вас есть базовое понимание того, как писать Swagger описание API. Это руководство помогает создавать и структурировать документацию API, что упрощает процесс его использования для других разработчиков. Вы можете расширять и улучшать документацию, добавляя дополнительные сведения, такие как параметры запроса, примеры ответов и многое другое.

### Дополнительные ресурсы

- [OpenAPI Specification](https://swagger.io/specification/)
- [Swagger Editor](https://editor.swagger.io/)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)
- [Swagger Codegen](https://swagger.io/tools/swagger-codegen/)