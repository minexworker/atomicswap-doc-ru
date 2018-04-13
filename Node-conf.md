# Кофигурирование кошелька

Чтобы начать процесс атомарного обмена, Minexcoin и Bitcoin кошельки должны быть правильно настроенными. Эта страница содержит руководство по настройке кошельков. Эта настройка применима для обоих криптовалют.

#### Тестовая сеть

Сперва нужно активировать **testnet** (тестовую сеть). Добавьте `testnet=1` в conf файл каждого кошелька. Или впишите это в командную строку во время запуска кошельков, например `minexcoind -testnet`

#### Данные RPC

Добавьте данные RPC в conf файлы как показано ниже:

```
rpcuser=my_user_name
rpcpassword=my_awesome_password
```

##### или

Впишите это в командною строку как показано ниже:

`minexcoind ... -rpcuser=my_user_name -rpcpassword=my_awesome_password`

Где `my_user_name` и `my_awesome_password` Ваши логин и пароль.

#### ZMQ

Добавьте ZMQ хост и номер порта для оповещений от кошелька в файле:

```
zmqpubhashblock=tcp://127.0.0.1:dddd
zmqpubhashtx=tcp://127.0.0.1:dddd
```

##### или

Кломандная строка:

`minexcoind ... -zmqpubhashblock=tcp://127.0.0.1:dddd -zmqpubhashtx=tcp://127.0.0.1:dddd`

Где `dddd` это номер порта (Число от 1024 до 65535 исключая числа с [этой таблицы](https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2_TCP_%D0%B8_UDP)).

#### Запуск в фоновом режиме

Это необязательный елемент. Включите это, если хотите запустить кошелек в фоновом режиме.

```
daemon=1
```

#### Заключение

Если все конфигурации сделаны, Ваш conf файл должен быть похож на это:

```
daemon=1
testnet=1
rpcuser=my_user_name
rpcpassword=my_awesome_password
zmqpubhashblock=tcp://127.0.0.1:dddd
zmqpubhashtx=tcp://127.0.0.1:dddd
```

Или командная строка на это:

```
minexcoind -testnet -rpcuser=my_user_name -rpcpassword=my_awesome_password \
-zmqpubhashblock=tcp://127.0.0.1:dddd -zmqpubhashtx=tcp://127.0.0.1:dddd
```