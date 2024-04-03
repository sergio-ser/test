# Home work

### Спроектируйте базу данных которая управляет пункт обмена валюты.

<br />

- База данных может иметь следующие таблицы:

```php
$tables = [
    'currencies', 
    'exchange_rates', 
    'operations', 
    'employees',
   ];
```

- Создайте необходимые миграции.
- Определите необходимые атрибуты (id, code, и т.д.) и отношения (1:n, n:m).
- Определите ограничения схемы базы данных (первичные ключи, внешние ключи, уникальность, индексы).
- Создайте возможность заполнения базы поддельными данными с помощью команды: <br>
`php artisan migrate –seed`

  <br/>

- Пункт будет работать со следующими валютами по отношению к молдавскому лею:

```php
$currencies = ['EUR', 'USD', 'RON'];
```

- Создайте задачу которая будет запускаться ежедневно и обновлять данные в таблице **exchange_rates**.

```php
$date = "01.01.2022"; // Date in d.m.Y format
$sourceUrl = "https://www.bnm.md/en/official_exchange_rates?get_xml=1&date=$date";
```

<br />

### Напишите API который будет следующий функционал:

- ежедневная история курса валют.
- список работников.
- валютные операции с данными на подобе:

```php
$operations = [{
    id: 1,
    currency_id: 2, // id of a currency, for example USD
    operation: 'buy', // or sell
    amount: 100, // amount of bought or sold currency
    operator_id: 5, // id of employee
}];
```

- возможность создания операции обмена методом **POST** (пример):

```php
$payload = [
    'currency' => 'USD',
    'operation' => 'sell', // or buy
    'amount' => 250,
    'operator_id' => 5, // id of employee
];
```

-  возможность получения курса определенной валюты за определенный день методом **GET** (пример):

```php
$payload = [
    'currency' => 'USD',
    'date' => '11.05.2022', // d.m.Y date format
];
```

- возможность просмотра операций методом **GET** по определенным критериям (пример):
```php
$payload = [
    'date' => '11.05.2022', // d.m.Y date format, mandatory field
    'operator_id' => 5, // id of employee, not mandatory
    'operation' => 'buy', // or sell, not mandatory, get all if not set
    'currency' => 'USD', // or another currency, not mandatory, return all if not set
];
```
