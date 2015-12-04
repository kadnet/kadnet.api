# Kadnet Api Клиент
С его помощью вы можете использовать сервис https://www.kadnet.ru для запроса сведений из Росреестра (далее РР) и отправки заявлений о постановке на кадастровый учет, доп. документов и прочее

####Авторизация пользователя
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
*Результат выполнения запроса*
```javascript
{  
   "Data":"dipjIB2lcWNwCgHGdjTAu9+VAGJHP2zhhdjdZCXNXkBMLT03HgI/eoLtbn76XZcsS+y11D4STA3qU3KAq1uUxD/dMmS2jjQ5YeQ8C2FHQi/8mwhMMZtIzp/PlydYRXBA/B+oia",
   "Date":"2015-12-04T14:57:42.1676008+03:00",
   "Result":true
}
```
###Запросы в Росреестр (КПТ, ЕГРП, КПЗУ, КВЗУ и прочие)
####Получить список типов запросов
```csharp
var requestsTypesResult = api.GetRequestsTypes();
```
*Результат выполнения запроса*
```javascript
{  
   "Result":true,
   "Data":[  
      {  
         "Id":"7f5891fe-9134-48ab-92a2-0b4c9ac5af08",
         "ShortTitle":"Выписка о переходе прав",
         "FullTitle":"Выписка о переходе прав объекта недвижимости"
      },
      {  
         "Id":"3fbfe5ff-0602-45e4-8434-aad052d7d234",
         "ShortTitle":"Выписка ЕГРП",
         "FullTitle":"Выписка о правах на объект недвижимости"
      },
      {  
         "Id":"66b36e90-30f6-4c74-8d20-eff440cc41ae",
         "ShortTitle":"КВЗУ",
         "FullTitle":"Кадастровая выписка земельного участка"
      },
      {  
         "Id":"a5b10384-95fe-4dba-887e-6ae5ff156f3f",
         "ShortTitle":"КП",
         "FullTitle":"Кадастровый паспорт"
      },
      {  
         "Id":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ShortTitle":"КПТ",
         "FullTitle":"Кадастровый план территории"
      },
      {  
         "Id":"31efe079-ea67-4fb8-9c9d-c38e194dba5c",
         "ShortTitle":"КСЗУ",
         "FullTitle":"Справка о кадастровой стоимости земельного участка"
      },
      {  
         "Id":"1b240b8e-a626-4305-9961-42e700a95e05",
         "ShortTitle":"Справка о лицах, получавших сведения",
         "FullTitle":"Справка о лицах, получивших сведения по объекту недвижимости"
      }
   ],
   "Date":"2015-12-04T14:57:42.8707956+03:00"
}
```
####Получить список типов объектов
```csharp
var objectTypesResult = api.GetObjectsTypes();
```
*Результат выполнения запроса*
```javascript
{  
   "Result":true,
   "Data":[  
      {  
         "Id":"1288670c-4a52-4ec7-b11b-a7ccdcc6c72f",
         "Title":"Земельный участок"
      },
      {  
         "Id":"204a4a4d-fb42-4ce1-bb03-0b5308b77ba0",
         "Title":"Здание"
      },
      {  
         "Id":"5790e1ad-4f46-4645-a832-1a60bca3bd5c",
         "Title":"Помещение"
      },
      {  
         "Id":"14aa88fe-ffa6-47cb-b8ff-9850b6802ccc",
         "Title":"Сооружение"
      },
      {  
         "Id":"ccbc177e-edd4-49a9-ba2b-5264f91b3410",
         "Title":"Объект незавершенного строительства"
      },
      {  
         "Id":"bbb11896-0141-4c50-b5d8-d0bc38cd5edd",
         "Title":"Предприятие как имущественный комплекс (ПИК)"
      },
      {  
         "Id":"e1356d06-12e8-49f7-8e91-b47f8913e6e3",
         "Title":"Участки недр"
      }
   ],
   "Date":"2015-12-04T15:09:34.9482977+03:00"
}
```
#####Получить список типов тарифных планов
```csharp
var requestsTariffsResult = api.GetRequestsTariffs();
var requestsTariffs = requestsTariffsResult.Data;
```
*Результат выполнения запроса*
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
