# kadnet.api
Kadnet Api Клиент. С его помощью вы можете использовать сервис https://www.kadnet.ru для запроса сведений из Росреестра (далее РР) и отправки заявлений о постановке на кадастровый учет, доп. документов и прочее

Авторизация пользователя
-----------
```csharp
var token;
var api = new KadnetApiClient(token);
var software = "CustomSoftware v3.1";
var login = "kadnet-test-user@gmail.com";
var password = "########";

var authResult = api.Auth(login, password, software);
if (authResult.Result)
  token = authResult.Data;
```

# Запросы в Росреестр (КПТ, ЕГРП, КПЗУ, КВЗУ и прочие)
Получить список запросов
-----------
```csharp
var limitRequests = 100;
var skipRequests = 0;
var requestsResult = api.GetRequests(limitRequests, skipRequests);
```

Получить запрос по идентификатору
-----------
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var requestResult = api.GetRequest(reqId);
```

Получить контент запрос для подписания ЭЦП пользователя
-----------
```csharp

```

Получить историю запроса по идентификатору
-----------
```csharp

```

Получить результат запроса
-----------
```csharp

```

Удалить запрос
-----------
```csharp

```

# Заявления в Росреестр (Доп. документы, постановка на кад.учет ЗУ и ОКС, Акты обследования и прочие)

Получить список заявлений
-----------
```csharp

```

Получить заявление по идентификатору
-----------
```csharp

```

Получить контент заявления для подписания ЭЦП пользователя
-----------
```csharp

```

Получить историю заявления по идентификатору
-----------
```csharp

```

Получить результат заявления
-----------
```csharp

```

Удалить заявление
-----------
```csharp

```
