<h2>Автоматизированные тесты в Postman<h2> 

![5b45245644bb575753f2fa08b758cab0](https://github.com/user-attachments/assets/b48d3dbb-0b44-42e5-9761-0cafd02ec4b6)

Как создать автоматизированный тест в Postman🖥️

1.Загрузите актуальную версию приложения с официального сайта, установите ее на свой компьютер и создайте учетную запись в Postman, если вы еще не зарегистрированы.

2.Войдите в приложение, выберите нужную коллекцию, директорию или запрос (в зависимости от теста), зайдите в раздел Scripts > Post-response в редакторе.Здесь вы можете написать собственный тест, используя JavaScript, или выбрать подходящий вариант в списке сниппетов с готовым кодом.

3.Отправьте запрос. Тест будет выполнен после выполнения запроса и получения ответа от API. Результат отобразится во вкладке Test Results.

> Ниже представлены примеры сценариев, которые можно использовать в компании интернет-провайдера

## Пример 1

## Важно: Убедиться, что API возвращает корректные данные о клиенте по его идентификатору.

Тестовый сценарий:
- Отправить GET запрос на эндпойнт /api/customers/{customerId}.
- Проверить, что статус ответа равен 200.
- Валидация структуры ответа (например, наличие полей id, name, email, status).

```
pm.test("Статус ответа 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Структура ответа корректна", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.all.keys('id', 'name', 'email', 'status');
});
```

## Пример 2

## Важно: Проверить, что можно успешно создать нового клиента через API.

Тестовый сценарий:
- Отправить POST запрос на эндпойнт /api/customers с необходимыми данными.
- Проверить, что статус ответа 201 Created.
- Убедиться, что в ответе присутствует id созданного клиента.

```
pm.test("Статус ответа 201", function () {
    pm.response.to.have.status(201);
});

pm.test("В ответе есть ID клиента", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
});
```

## Пример 3

## Важно: Убедиться, что можно изменить статус интернет-услуги клиента (например, активировать или деактивировать).

Тестовый сценарий:
- Отправить PUT запрос на эндпойнт /api/customers/{customerId}/services/{serviceId} с новым статусом.
- Проверить, что статус ответа 200.
- Проверить, что статус услуги обновлен в ответе.

```
pm.test("Статус ответа 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Статус услуги обновлен", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.status).to.eql("active"); // или "inactive"
});
```

## Пример 4

## Важно: Убедиться, что API корректно генерирует счет для клиента.

Тестовый сценарий:
- Отправить GET запрос на эндпойнт /api/customers/{customerId}/billing.
- Проверить, что статус ответа 200.
- Валидация полей счета, например invoiceId, amount, dueDate.

```
pm.test("Статус ответа 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Счет содержит необходимые поля", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.all.keys('invoiceId', 'amount', 'dueDate', 'status');
});
```

## Пример 5

## Важно: Убедиться, что время ответа API находится в допустимых пределах (например, менее 500 мс).

Тестовый сценарий:
- Отправить любой запрос к API.
- Проверить, что время ответа не превышает 500 мс.

```
pm.test("Время ответа менее 500 мс", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

## Пример 6

## Важно: Убедиться, что без корректного токена авторизации доступ к защищённым ресурсам запрещён.

Тестовый сценарий:
- Отправить GET запрос на эндпойнт /api/customers/{customerId} без заголовка авторизации.
- Проверить, что статус ответа 401 Unauthorized.

```
pm.test("Отказано в доступе без авторизации", function () {
    pm.response.to.have.status(401);
});

```

Эти примеры помогут обеспечить качество и надёжность API, используемого в компании интернет-провайдера. Вы можете расширять их в зависимости от специфики вашего проекта и дополнительных требований
