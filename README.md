# Kadnet Api Клиент     

С помощью данного API клиента вы можете использовать сервис https://www.kadnet.ru 
для запроса сведений из Росреестра (далее РР) и отправки заявлений о постановке на кадастровый учет, 
доп. документов и т.д.

1. Общие методы
 + [Авторизация пользователя](#Parag);

2. Отправка запросов в Росреестр (КПТ, ЕГРП, КПЗУ, КВЗУ и прочие)
 + [Получить список типов запросов](#GetRequestsTypes);
 + [Получить список типов объектов ГКН](#GetObjectsTypesGkn);
 + [Получить список типов объектов ЕГРП](#GetObjectsTypesEgrp);
 + [Получить список типов тарифных планов](#GetRequestsTariffs);
 + [Проверить кадастровый номер](#CheckRequests);
 + [Создать новый запрос в РР](#CreateRequest);
 + [Получить список запросов для подписания ЭЦП пользователя](#GetRequestsToSign);
 + [Сохранить подпись запроса](#SaveSign);
 + [Получить список запросов](#GetRequests);
 + [Получить запрос по идентификатору](#GetRequest);
 + [Получить историю запроса по идентификатору](#GetRequestHistory);
 + [Получить результат запроса](#GetRequestContent);

3. Отправка заявлений в Росреестр
 + [Получить список заявлений](#);
 + [Получить заявление по идентификатору](#);
 + [Получить контент заявления для подписания ЭЦП пользователя](#);
 + [Получить историю заявления по идентификатору](#);
 + [Получить результат заявления](#);
 + [Удалить заявление](#);


####<a name="Auth"></a>Авторизация пользователя
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

####<a name="GetRequestsTypes"></a>Получить список типов запросов
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

####<a name="GetObjectsTypesGkn"></a>Получить список типов объектов ГКН
```csharp
var objectTypesResult = api.GetObjectsTypesGkn();
```
*Результат выполнения запроса*
```javascript
{
	"Result": true,
	"Data": [{
		"Id": "1288670c-4a52-4ec7-b11b-a7ccdcc6c72f",
		"Title": "Земельный участок"
	}, {
		"Id": "204a4a4d-fb42-4ce1-bb03-0b5308b77ba0",
		"Title": "Здание"
	}, {
		"Id": "5790e1ad-4f46-4645-a832-1a60bca3bd5c",
		"Title": "Помещение"
	}, {
		"Id": "14aa88fe-ffa6-47cb-b8ff-9850b6802ccc",
		"Title": "Сооружение"
	}, {
		"Id": "ccbc177e-edd4-49a9-ba2b-5264f91b3410",
		"Title": "Объект незавершенного строительства"
	}, {
		"Id": "bbb11896-0141-4c50-b5d8-d0bc38cd5edd",
		"Title": "Предприятие как имущественный комплекс (ПИК)"
	}, {
		"Id": "e1356d06-12e8-49f7-8e91-b47f8913e6e3",
		"Title": "Участки недр"
	}],
	"Date": "2016-02-04T09:50:12.0232985+03:00"
}
```
####<a name="GetObjectsTypesEgrp"></a>Получить список типов объектов ЕГРП
```csharp
var objectTypesResult = api.GetObjectsTypesEgrp();
```
*Результат выполнения запроса*
```javascript
{
	"Result": true,
	"Data": [{
		"Id": "1288670c-4a52-4ec7-b11b-a7ccdcc6c72f",
		"Title": "Земельный участок"
	}, {
		"Id": "7b29e86b-c5ec-41f3-aaf5-b8f511600cb3",
		"Title": "Квартира"
	}, {
		"Id": "91aa7b6c-bb8e-438a-a57b-9d452abebde9",
		"Title": "Комната"
	}, {
		"Id": "54f52d6b-3f70-4e3d-8137-d7f7fc55c89e",
		"Title": "Помещение не жилое"
	}, {
		"Id": "b3c8d68b-796c-4cf4-b06a-1b46ef5d0c1b",
		"Title": "Здание жилое"
	}, {
		"Id": "f2ed2c39-eb4b-4190-956b-38462bc48709",
		"Title": "Здание не жилое"
	}, {
		"Id": "14aa88fe-ffa6-47cb-b8ff-9850b6802ccc",
		"Title": "Сооружение"
	}, {
		"Id": "ccbc177e-edd4-49a9-ba2b-5264f91b3410",
		"Title": "Объект незавершенного строительства"
	}, {
		"Id": "bbb11896-0141-4c50-b5d8-d0bc38cd5edd",
		"Title": "Предприятие как имущественный комплекс (ПИК)"
	}, {
		"Id": "e1356d06-12e8-49f7-8e91-b47f8913e6e3",
		"Title": "Участки недр"
	}],
	"Date": "2016-02-04T10:02:06.3759783+03:00"
}
```

####<a name="GetRequestsTariffs"></a>Получить список типов тарифных планов
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
         "TariffCode":"KptAllInclusive",
         "UserDescription":"190 рублей - Автоматическая оплата"
      },
      {  
         "TariffCode":"KptItSelf2015",
         "UserDescription":"10Р + Самостоятельная оплата по коду платежа"
      },
      {  
         "TariffCode":"EgrpItSelfSummer2015",
         "UserDescription":"Самостоятельная оплата по коду платежа в Qiwi"
      },
      {  
         "TariffCode":"EgrpAllInclusive",
         "UserDescription":null
      },
      {  
         "TariffCode":"EgrpLite",
         "UserDescription":null
      }
   ],
   "Date":"2015-12-04T15:09:36.0421248+03:00"
}
```


####<a name="CheckRequests"></a>Проверить кадастровый номер
```csharp
var kadNubmers = "24:50:0000000:58340;24:50:0000000:58360-58365";
var comment = "Иванов И.И., договор №3315";
var requestsTypeId = Guid.Parse("6aa0e204-4d11-4e97-8348-1c2d9bce3655");//КПТ
var objectTypeId = Guid.Empty;
var checkRequestsResult = api.CheckRequests(kadNubmers, comment, requestsTypeId, objectTypeId);
var checkRequests = checkRequestsResult.Data;

JArray json = JArray.Parse(checkRequests);
```
*Результат выполнения запроса*
```javascript
{  
   "Result":true,
   "Data":[  
      {  
         "DT_RowId":"b921dd77-ad44-4489-8200-3e321c2894e2",
         "Number":"24:50:0000000:58340",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Железнодорожников, д. 30, кв. 48",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"c8db5f32-be2f-4e69-9d9d-f1a5f95a4838",
         "Number":"24:50:0000000:58360",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв.150",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"7f727a86-2837-4e9d-9af3-f564a1679928",
         "Number":"24:50:0000000:58361",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв. 1",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"8504a3f6-f147-4653-87e9-754a6b314995",
         "Number":"24:50:0000000:58362",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв. 4",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"5c683f9f-0ea7-4d47-ac83-f8b4a1282cb3",
         "Number":"24:50:0000000:58363",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв. 39",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"a05dcc49-7b11-4272-ae27-fb3b004d8565",
         "Number":"24:50:0000000:58364",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв. 152",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      },
      {  
         "DT_RowId":"b31c2233-106e-48a5-af95-48ee56b33eaa",
         "Number":"24:50:0000000:58365",
         "Comment":"Иванов И.И., договор №3315",
         "Info":"Красноярский край, г. Красноярск, ул. Копылова, д. 78, кв. 3",
         "Type":"6aa0e204-4d11-4e97-8348-1c2d9bce3655",
         "ObjectType":"00000000-0000-0000-0000-000000000000"
      }
   ],
   "Date":"2015-12-04T16:36:54.3029506+03:00"
}
```
              
####<a name="CreateRequest"></a>Создать новый запрос в РР
```csharp
var kadNubmer = "66:41:10204:003";
var selfSignedRequest = false;
var tariffCode = "KptAllInlusive";
var createRequestResult = api.CreateRequest(selfSignedRequest, tariffCode, kadNubmer, comment, requestsTypeId, objectTypeId);
var createRequest = createRequestResult.Data;
```
*Результат выполнения запроса*
```javascript

```

####<a name="GetRequestsToSign"></a>Получить список запросов для подписания ЭЦП пользователя
```csharp
var requestsToSignResult = api.GetRequestsToSign();
var requestsToSign = requestsToSignResult.Data;
```
*Результат выполнения запроса*
```javascript

```

####<a name="SaveSign"></a>Сохранить подпись запроса
```csharp
var requestId = Guid.Empty;
var signContent = "base64";
var certContent = "base64certificate";
var cpVersion = "CryptoPro version";

var saveSignResult = api.SaveSign(requestId, signContent, certContent, cpVersion);
var saveSign = saveSignResult.Data;
```
*Результат выполнения запроса*
```javascript

```

####<a name="GetRequests"></a>Получить список запросов
```csharp
var limitRequests = 100;
var skipRequests = 0;
var requestsResult = api.GetRequests(limitRequests, skipRequests);
```
*Результат выполнения запроса*
```javascript

```

####<a name="GetRequest"></a>Получить запрос по идентификатору
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var requestResult = api.GetRequest(reqId);
var request = requestResult.Data;
```
*Результат выполнения запроса*
```javascript

```

####<a name="GetRequestHistory"></a>Получить историю запроса по идентификатору
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var historyResult = api.GetRequestHistory(reqId);
var history = historyResult.Data;
```
*Результат выполнения запроса*
```javascript

```

####<a name="GetRequests"></a>Получить результат запроса
```csharp     
//получить результат запроса
var requestBodyResult = api.GetRequestContent(reqId, ExportFormat.Raw);

//получить результат запроса в CAD формате
var requestBodyResultDxf = api.GetRequestContent(reqId, ExportFormat.Dxf);

//получить результат запроса в Mid/Mif формате
var requestBodyResultMidMif = api.GetRequestContent(reqId, ExportFormat.MidMif);

//получить результат запроса в Pdf формате
var requestBodyResultPdf = api.GetRequestContent(reqId, ExportFormat.Pdf);

//Для КПТ можно получить список пунктов ОМС
var requestBodyResultOmsPoints = api.GetRequestContent(reqId, ExportFormat.OmsPoints);

```
*Результат выполнения запроса*
```javascript

```
#####Удалить запрос
```csharp
var reqId = Guid.Parse("C1231EF4-DBD4-479C-A68A-033F47D9E237");
var deleteResult = api.DeleteRequest(reqId);
var delete = deleteResult.Data;
```
*Результат выполнения запроса*
```javascript

```

###Заявления в Росреестр (Доп. документы, постановка на кад.учет ЗУ и ОКС, Акты обследования и прочие)

####<a name=""></a>Получить список заявлений
```csharp

```
*Результат выполнения запроса*
```javascript

```
####<a name=""></a>Получить заявление по идентификатору
```csharp

```
*Результат выполнения запроса*
```javascript

```
####<a name=""></a>Получить контент заявления для подписания ЭЦП пользователя
```csharp

```
*Результат выполнения запроса*
```javascript

```
####<a name=""></a>Получить историю заявления по идентификатору
```csharp

```
*Результат выполнения запроса*
```javascript

```

####<a name=""></a>Получить результат заявления
```csharp

```
*Результат выполнения запроса*
```javascript

```

####<a name=""></a>Удалить заявление
```csharp

```
*Результат выполнения запроса*
```javascript

```
