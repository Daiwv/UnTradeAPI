# Модуль для работы с биржами.

Язык: Python 3.4 

Поддерживаются биржы Exmo и BTC-e. Цель данного модуля - построение универсального интерфейса для бирж.

# Использование

```
import exchange

exmo = exchange.exchange_exmo({'key': '', secret': ''})
btce = exchange.exchange_btce({'key': '', secret': ''})
polo = exchange.exchange_poloniex({'key': '', secret': ''})
```

Обращаться к API можно двумя способами:
- прямое обращение к API биржы - ```exmo.do.имяМетода() или exmo.do._имяМетода()``` - Символ подчёркивания означает метод, использующий авторизацию, без подчёркивания - без авторизации. Полный список методов можно найти в документации соответствующих бирж.
- универсальные методы - ```exmo.имяФункции()``` - вне зависимости от биржы.

Функции обеих катагорий возвращают три значения: результат, наличие ошибки, список ошибок. Всегда в таком порядке

Примеры прямого обращения к биржам:
```
exmo.do._user_info() # запрос информации 
btce.do._getInfo() # то же самое

btce.do.info(pairs=['usd_rur']) # информация о торгах по валютным парам
exmo.do.order_book(pair='USD_RUB', limit=10) # то же самое
```

Функции прямого обращения к API используют разные (хотя и похожие) форматы названия валютных пар. Но универсальные функции - один способ для всех бирж: латнискими буквами в нижнем регистре, в качестве разделителя валют - знак тире. Необходимо всё же понимать, что хотя универсальные функции и возвращают результат в одинаковом формате, но одни биржы предоставляют некоторую инфорацию, а другие - нет.

Обращение к API через универсальные функции. Вместо "exmo" можно подставлять любую биржу.

```
exmo.price('btc-usd') # получение цены пары. Для Exmo можно указать второй аргумент - количество значений в "стакане"
id_order = e.new_order('usd-rur', 'sell') # Создание ордера
```

# Подробнее про универсальные функции

Получение цены:

data, success, errors = exmo.price('usd-rur') - в качестве data будет возвращён объект Price, имеющего следующие свойства:
- data.sell - цена продажи
- data.buy - цена покупки
- data.spread() - спрэд (цена покупки - цена продажи)

Создание ордера

data, success, errors = exmo.create_order(pair, action, quantity, price) - в качестве data будет возвращён код ордера. Для совершения купли/продажи по рыночной стоимости вместо цены необходимо указать ключевое слово "market".




 
 
 
------------------------------- ещё не сделано :( 
e.price('usd_rur', 'buy')
id_order = e.new_order('usd_rur', 'sell')
id_order = e.new_order('usd_rur', 'buy')
e.cancel_order(id_order)