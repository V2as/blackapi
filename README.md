## Коды
**201**: Сценарий выполнен по правилам
**500**: Внутренняя техническая ошибка
**401**: Cинтаксическая ошибка


## Статусы

### `status` Статус выполнения сценария
**'success'**:str Сценарий с регистрацией или передачей значения выполнен по правилам 
**'done'**:str Сценарий с выполнением автоматизации выполнен по правилам
**'fail'**:str Сценарий выполнен с ошибкой
**'bad json params'**:str Сценарий при котором json неправильно составлен для запроса


### Если `status` **fail**, можно получить `error`: Вывод подробностей ошибки
> REST API написан на python, из этого статуса можно получить краткое описание ошибки кода


## API запросы и ответы

### Создание ключа (Key creation)
`post` <code>/api/makeKey</code>
```python
{'user_id':str
 'role':str}
```
`return`
```python 
{'status':str
 'key':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`role`: Тариф, на английском языке
`key`: Зашифрованный ключ для приложения AmneziaVPN 


### Смена ключа (Key changing)
> Удаление старого ключа, создание нового ключа

`post` `/api/changeKey`
```python
{'user_id':str
 'role':str}
```
`return`
```python 
{'status':str
 'key':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`role`: Тариф, на английском языке
`key`: Зашифрованный ключ для приложения AmneziaVPN 


### Смена страны 
> Удаление стаорого ключа с тарифом **MYSTERY**, создание нового ключа
 
`post` `/api/changeCountry`
```python
{'user_id':str
 'country':str}
```
`return`
```python 
{'status':str
 'key':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`country`: Страна, на русском языке
`key`: Зашифрованный ключ для приложения AmneziaVPN 


### Получение ключа 
`post` `/api/getKey`
```python
{'user_id':str}
```
`return`
```python 
{'status':str
 'key':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`key`: Зашифрованный ключ для приложения AmneziaVPN 


### Получение личного кабинета
`post` `/api/getCabinet`
```python
{'user_id':str}
```
`return`
```python
{'id':str,
 'user_id':str,
 'free':float,
 'balance':float,
 'tarif':str,
 'register':int,
 'status':int,
 'refid':str,
 'last_pay':str,
 'tarif_until':str,
 'ip':str,
 'refcount':int,
 'country':str,
 'status':str'}
 ```
 `id`: (Не нужно, скоро уберу),
 `user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*,
 `free`: Сумма ежедневного списания,
 `balance`: Баланс клиента,
 `tarif`: Тариф клиента, написанный большими английскими буквами,
 `register`: Статус клиента, определяющий количество смен тарифа,
 `status`: Статус клиента в системе (если 0-4, где 4 полная блокировка, нужно только для *Telegram*),
 `refid`: Реферал, к которому будет приходить процент от суммы пополнения клиентом,
 `last_pay`: Наименование сервиса, в котором зарегистрировался клиент,
 `tarif_until`: Наименование дополнительного кабинета (любые символы),
 `ip`: IP адресс сервера, на котором расположен [peer] клиента,
 `refcount`: Количество приглашенных рефералов,
 `country`: Страна (если есть) из конфигурации


### Получение ссылки с платёжной формой
`post` `/api/makePay`
```python
{'user_id':str:
 'summ':int,
 'email':str,
 'app':str}
```
`return`
```python
{'status':str
 'url':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*,
`summ`: Сумма для пополнения баланса клиента в рублях,
`email`: Электронная почта клиента, на которую придет чек,
`app`: Проект, с которого клиент пришел пополнять баланс


### Получение списка стран
`post` `/api/showCountries`
```python
 {'role':str}
```
`return`
```python 
{'status':str
 'countries':{'name':str
              'path':str}}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`role`: Тариф, на английском языке
`countries`: Список стран нахождений серверов тарифа


### Получение списка тарифов
`post` `/api/showRoles`
`return`
```python 
{'status':str
 'roles':{'name':str
          'price':float}}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`roles`: Список тарифов серверов

### Создание русского ключа
`post` `/api/makeRusKey`
```python
{'user_id':str}
```
`return`
```python 
{'status':str
 'key':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*
`key`: Зашифрованный ключ для приложения AmneziaVPN 


### Удаление русского ключа 
`post` `/api/deleteRusKey`
```python
{'user_id':str}
```
`return`
```python 
{'status':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*


### Удаление ключа 
> Отличается тем, что задействует методы удаления ключа из базы данных, тем временем, как русский ключ не записывается в базу данных. В основном русский ключ опционален только для *Black Temple*
`post` `/api/deleteKey`
```python
{'user_id':str}
```
`return`
```python 
{'status':str}
```
`user_id`: Уникальный индефикатор клиента в базе данных, созданный с помощью *Telegram*

## Методы работы с почтой и паролем


### Регистрация
> После регистрации у пользователя в базе данных статус 401, то есть "неподтвержденный аккаунт", важно вызвать метод `/api/logInAccessBegin` чтобы отправить письмо с подтверждением на почту, а после подтверждения вызвать `/api/logInAccessEnd`

`post` `/api/logIn`
```python
{'email':str
 'password':str}
```
`return`
```python 
{'status':str
 'message':str}
```
> При попытке передать почту, которая уже зарегистрирована в системе, будет показан status fail 
`email`: Электронная почта клиента, может выступать логином
`password`: Пароль от аккаунта клиента


### Отправка письма с подтверждением регистрации

> После регистрации у пользователя в базе данных статус 401, то есть "неподтвержденный аккаунт", важно вызвать метод `/api/logInAccessBegin`

`post` `/api/logInAccessBegin`
```python
{'email':str
 'password':str}
```
`return`
```python 
{'status':str}
```
> При попытке передать почту, которая уже зарегистрирована в системе, будет показан status fail

`email`: Электронная почта клиента, может выступать логином
`password`: Пароль от аккаунта клиента


### Подтверждение регистрации

> Чтобы подтвердить регистрацию, надо передать json запрос с id клиента и email (Можно убрать эту схему)

`post` `/api/logInAccessEnd`
```python
{'email':str
 'id':str}
```
`return`
```python 
{'status':str}
```
`email`: Электронная почта клиента, может выступать логином
`id`: Уникальный индефикатор
