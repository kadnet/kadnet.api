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
Получить список запросов в РР
-----------
```csharp
var limitRequests = 100;
var skipRequests = 0;
var requestsResult = api.GetRequests(limitRequests, skipRequests);
```

Получить запрос в РР по идентификатору
-----------
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var requestResult = api.GetRequest(reqId);
```
