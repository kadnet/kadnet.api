# kadnet.api
Kadnet Api Клиент. С его помощью вы можете использовать сервис https://www.kadnet.ru для запроса сведений из Росреестра и отправки заявлений о постановке на кадастровый учет, доп. документов и прочее

авторизация пользователя
-----------

```
var token;
var api = new KadnetApiClient(token);
var software = "CustomSoftware v3.1";
var login = "kadnet-test-user@gmail.com";
var password = "########";

var authResult = api.Auth(login, password, software);
  if (authResult.Result)
    token = authResult.Data;
```
