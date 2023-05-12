# T-Meteo-API

Данные из сервиса погодавполе.рф 
T-Meteo API позволяет получать показания метеостанций T-Meteo, подлюченных к сервису https://погодавполе.рф в режиме реального времени.
T-Meteo API использует протокол HTTP JSON. Данные передаются по протоколу HTTP, защищенному SSL. Все методы возвращают данные в формате JSON.
T-Meteo API версии 1 доступен по следующим адресам:
https://api.погодавполе.рф 
https://api.ttrackagro.ru
Авторизация
Для получения доступа к системе ко всем HTTP запросам нужно добавлять HTTP-заголовок 'X-Token-Auth' со значением токена авторизации. В версии API 1.0 получение токена по имени пользователя и паролю не предусмотрено. Вместо этого, обратитесь к разработчику для получения токена.
Clients 
https://api.погодавполе.рф/clients
https://api.ttrackagro.ru/clients

Получить список всех клиентов (учетных записей погодавполе.рф) к которым у вас есть доступ.
Возвращаемые поля:
~~~
[
    {
        "id": "id клиента",
        "name": "Название клиента"
    }
]
~~~
  id - uuid клиента
  name - наименование клиента в системе


Devices 
https://api.погодавполе.рф/devices
https://api.ttrackagro.ru/devices
Получить список всех устройств подключенных к погодавполе.рф к которым у вас есть доступ.
Возвращаемые поля:
~~~
[
    {
        "id": "id устройства",
        "name": "Внутреннее имя устройства (уникальное)",
        "label": "Имя устройства у клиента",
        "client_id": "id клиента",
    }
]
~~~
  id - uuid устройства
  name - уникальное внутреннее наименование устройства, строка до 16 символов в формате [Модель устройства]-[Серийный номер]
  label - клиентское наименование - именно под этим именем видит устройство клиент. Если не заполнено, то используется внутреннее наименование
  client_id - uuid клиента, которому принадлежит устройство


Sensors 
https://api.погодавполе.рф/devices
https://api.ttrackagro.ru/sensors
Получить список всех возможных датчиков устройств с пояснениями о том, что показывает тот или иной датчик
Возвращаемые поля:
~~~
{
  "airtemp": "Температура воздуха, °C",
  "soiltemp": "Температура почвы, °C",
  "rainfall": "Количество выпавших осадков, мм",
  "soilmoist1": "Влажность почвы (капиллярная составляющая потенциала почвенной влаги): датчик №1 (рекомендованная глубина - до 20 см), сбар",
  "soilmoist2": "Влажность почвы (капиллярная составляющая потенциала почвенной влаги): датчик №2 (рекомендованная глубина - 40 см), сбар",
  "soilmoist3": "Влажность почвы (капиллярная составляющая потенциала почвенной влаги): датчик №3 (рекомендованная глубина - 60 см), сбар",
  "airTempMin": "Минимальная суточная температура воздуха, °C",
  "airTempAvg": "Средняя суточная температура воздуха, °C",
  "airTempMax": "Максимальная суточная температура воздуха, °C",
  "sat5": "Текущая сумма активных температур воздуха свыше 5°C с начала года/момента установки станции",
  "sat10": "Текущая сумма активных температур воздуха свыше 10°C с начала года/момента установки станции",
  "windang": "Направление ветра в градусах (0..337,5) - один из 16 румбов",
  "windspeed": "Скорость ветра, м/с",
  "windspeedmax": "Порывы ветра, м/с",
  "position.latitude": "Географическая широта места нахождения станции, °",
  "position.longitude": "Географическая долгота места нахождения станции, °"
}
~~~

Telemetry 
https://api.погодавполе.рф/telemetry?from=1648760400000&to=1648846799999
https://api.ttrackagro.ru/telemetry?from=1648760400000&to=1648846799999
Получить показания телеметрии (значений датчиков) устройств за заданный промежуток времени. Промежуток времени задается HTTP параметрами From и To в виде количества милисекунд прошедших от 01.01.1970 00:00:00. Иными словами, unix-timestamp в милисекундах. Например, момент времени 01 июня 2021 года 12:00:00 GMT+3 будет равен 1622538000000
Параметры:
  from - начало периода, за который получаются показания, число милисекунд
  to - окончание периода, за который получаются показания, число милисекунд
Возвращаемые поля:
~~~
[
    {
        "id": "id устройства",
        "key": "Название датчика",
        "ts": "UNIX-timestamp",
        "value": "Показания датчика",
    }
]
~~~
  id - uuid устройства
  key - наименование датчика, строка (см. метод Sensors 
  ts - дата и время показания, аналогично входным параметрам
  value - значение показания датчика, число до 2х знаков после запятой
