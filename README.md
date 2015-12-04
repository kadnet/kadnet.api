# Kadnet Api Клиент
С его помощью вы можете использовать сервис https://www.kadnet.ru для запроса сведений из Росреестра (далее РР) и отправки заявлений о постановке на кадастровый учет, доп. документов и прочее

#####Авторизация пользователя
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

###Запросы в Росреестр (КПТ, ЕГРП, КПЗУ, КВЗУ и прочие)
#####Получить список типов запросов
```csharp
var requestsTypesResult = api.GetRequestsTypes();
```
#####Получить список типов объектов
```csharp
var objectTypesResult = api.GetObjectsTypes();
```
#####Получить список типов тарифных планов
```csharp
var requestsTariffsResult = api.GetRequestsTariffs();
var requestsTariffs = requestsTariffsResult.Data;
```
```javascript
{
  "Result":true,
  "Data":[
    {
      "TariffCode":"KptItSelf2015",
      "UserDescription":"10Р + Самостоятельная оплата по коду платежа"
    },
    {
      "TariffCode":"KptAllInclusive",
      "UserDescription":"190 рублей - Автоматическая оплата"
    }
  ]
}
```


#####Проверить кадастровый номер
```csharp
var kadNubmers = "66:41:10204:003-005;";
var comment = "Обухово, клиент Иванов";
var requestsTypeId = Guid.Parse("6aa0e204-4d11-4e97-8348-1c2d9bce3655");//КПТ
var objectTypeId = Guid.Empty;
var checkRequestsResult = api.CheckRequests(kadNubmers, comment, requestsTypeId, objectTypeId);
var checkRequests = checkRequestsResult.Data;

JArray json = JArray.Parse(checkRequests);
```
#####Создать новый запрос в РР
```csharp
var kadNubmer = "66:41:10204:003";
var selfSignedRequest = false;
var tariffCode = "KptAllInlusive";
var createRequestResult = api.CreateRequest(selfSignedRequest, tariffCode, kadNubmer, comment, requestsTypeId, objectTypeId);
var createRequest = createRequestResult.Data;
```
#####Получить список запросов для подписания ЭЦП пользователя
```csharp

```
#####Сохранить подпись запроса
```csharp

```
#####Получить список запросов
```csharp
var limitRequests = 100;
var skipRequests = 0;
var requestsResult = api.GetRequests(limitRequests, skipRequests);
```
#####Получить запрос по идентификатору
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var requestResult = api.GetRequest(reqId);
var request = requestResult.Data;
```
#####Получить историю запроса по идентификатору
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var historyResult = api.GetRequestHistory(reqId);
var history = historyResult.Data;
```
#####Получить результат запроса
```csharp

```
#####Удалить запрос
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var deleteResult = api.DeleteRequest(reqId);
var delete = deleteResult.Data;
```

###Заявления в Росреестр (Доп. документы, постановка на кад.учет ЗУ и ОКС, Акты обследования и прочие)
#####Получить список заявлений
```csharp

```
#####Получить заявление по идентификатору
```csharp

```
#####Получить контент заявления для подписания ЭЦП пользователя
```csharp

```
#####Получить историю заявления по идентификатору
```csharp

```
#####Получить результат заявления
```csharp

```
#####Удалить заявление
```csharp

```
