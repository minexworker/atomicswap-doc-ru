# Запуска атомарного обмена как библиотеки

Перед настройкой кода атомарного обмена посмотрите руководство по [конфигурированию кошелька](Node-conf.md).

## Настройка

Все настройки раположены в главной функции. Измените их в соответствии с Вашей ситуацией и системной средой.

### Пример

Давайте представим, что мы делаем атомарный обмен между блокчейнами Minexcoin и Bitcoin. Параметры настройки описаны ниже. Настройка делится на две части - для Вас (`A`) и для Вашего партнера (`B`). Каждый участник должен настроить обе части, но в разном порядке.

В этом примере `A` отправляет Minexcoin и получает Bitcoin. `B` наоборот.

##### Настройки для `A`
IP адрес и номер порта `A` для соединения с `B` через сокет:
```java
selfData.inetAddress(new InetSocketAddress("ddd.ddd.ddd.ddd", dddd));
```

IP адрес и номер порта RPC Minexcoin кошелька:
```java
selfData.nodeAddress(new InetSocketAddress("127.0.0.1", 17788));
```

Логин и пароль для RPC Minexcoin кошелька:
```java
selfData.nodeLogin("user");
selfData.nodePassword("password");
```

Номер порта для ZMQ оповещений от Minexcoin кошелька:
```java
selfData.notificationPort(1112);
```

Количество монет Minexcoin для отправки (в satoshi):
```java
selfData.amount(Coin.valueOf(1000000000));
```

Приватный ключ (несжатый, HEX) `A` для Minexcoin адреса:
```java
selfData.myKey(ECKey.fromPrivate(new BigInteger("<private_key_here>", 16), false));
```

Публичный ключ (несжатый, HEX) `B` для Minexcoin адреса:
```java
selfData.otherKey(ECKey.fromPublicOnly(new BigInteger("<public_key_here>", 16).toByteArray()));
```

Экземпляр класса для работы с блокчейном Minexcoin:
```java
selfData.worker(MinexCoinWorker.instance());
```

Количество подтверждений для предположения того, что транзакция Minexcoin зрелая и количество подтверждений (CSV) для того, чтобы сделать возврат средств:
```java
selfData.confirmations(2);
selfData.csv(3);
```

Настройка параметров для партнера очень похожа за исключением аспектов блокчейна другой криптовалюты.

##### Настройки для `B`

IP адрес и номер порта `B` для соединения с `A` через сокет:
```java
partnerData.inetAddress(new InetSocketAddress("ddd.ddd.ddd.ddd", dddd));
```

IP адрес и номер порта RPC Bitcoin кошелька:
```java
partnerData.nodeAddress(new InetSocketAddress("127.0.0.1", 18332));
```

Логин и пароль для RPC Bitcoin кошелька:
```java
partnerData.nodeLogin("user");
partnerData.nodePassword("password");
```

Номер порта для ZMQ оповещений от Bitcoin кошелька:
```java
partnerData.notificationPort(1113);
```

Количество монет Bitcoin для получения (в satoshi):
```java
partnerData.amount(Coin.valueOf(1000000000));
```

Приватный ключ (несжатый, HEX) `A` для Bitcoin адреса:
```java
partnerData.myKey(ECKey.fromPrivate(new BigInteger("<private_key_here>", 16), false));
```

Публичный ключ (несжатый, HEX) `B` для Bitcoin адреса:
```java
partnerData.otherKey(ECKey.fromPublicOnly(new BigInteger("<public_key_here>", 16).toByteArray()));
```

Экземпляр класса для работы с блокчейном Bitcoin:
```java
partnerData.worker(BitcoinWorker.instance());
```

Количество подтверждений для предположения того, что транзакция Bitcoin зрелая и количество подтверждений (CSV) для того, чтобы сделать возврат средств:
```java
partnerData.confirmations(2);
partnerData.csv(3);
```

## Запуск

Приложение основано на Конечном Автомате (FSM) с реактивным подходом.

Для запуска FSM Вы должны сначала настроить параметры selfDara и partnerData. Вы можете посмотреть а файл [App.java](https://github.com/minexcoin/atomicswap/blob/master/src/main/java/com/minexcoin/atomic_swap/App.java) для примера. Но используйте только один случай для настройки.

После этого создайте новый экземаляр AtomicSwapFSM:
```java
final FSM<TxState<TxStatus>> fsm = AtomicSwapFSM.create(
	selfData, partnerData,
	true,
	5, TimeUnit.SECONDS,
	5, TimeUnit.SECONDS,
	1000, "AtomicSwapFSM Event", "AtomicSwapFSM-Task-%d"
);
```

И, наконец, запустите процесс атомарного обмена:
```java
fsm.start();
```