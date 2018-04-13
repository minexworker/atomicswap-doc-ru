# Описание GUI атомарного обмена

Процесс атомарного обмена требует установки определенного количества параметров. Довольно неудобно устанавливать их прямо в коде. Для того, чтобы сделать процесс атомарного обмена более дружелюбным, был разработан GUI. Однако GUI формы имеют множество полей.

Здесь приведено описание компонентов GUI атомарного обмена.

### IP адреса

Сначала нужно установить IP адреса обоих пользователей. Для этой цели служат два блока с полями, названные **My inet settings** и **Partner inet settings**. В этих блоках указываются Ваши IP адрес(названный *Host*) и номер порта(названный *Port*), и Вашего партнера соответственно.

Номер порта может быть случайным числом, но убедитесь в том, что это число лежит в диапазоне чисел от 1024 до 65535 и не совпадает с любым номером порта с [этой таблицы](https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D0%BE%D1%80%D1%82%D0%BE%D0%B2_TCP_%D0%B8_UDP).

Предоставьте свой IP адрес и номер порта Вашему партнеру и попросите его сделать также для Вас. И заполните каждое поле с каждого блока.

Подсказка: *Если Вы не знаете свой IP адрес, Вы можете посетить любой ресурс, который отображает Ваш IP адрес, например [ICanHazIP](http://icanhazip.com/)*.

### Minexcoin настройки

Блок полей с названием **Minexcoin settings** должен содержать данные, которые относятся к Вашему minexcoin кошельку. Описание каждого из полей приведено ниже.

Подсказка: *Перед заполнением некоторых из приведенных ниже полей сначала прочтите руководство по [конфигурированию кошелька](Node-conf.md) для правильной настройки Вашего кошелька*.

**Login** - данные для доступа к RPC, должен быть равным параметру "rpcuser", что обозначен в файле конфигурации или в командной строке при запуске кошелька.

**Password** - данные для доступа к RPC, должен быть равным параметру "rpcpassword", что обозначен в файле конфигурации или в командной строке при запуске кошелька.

**Notification port** - номер порта ZMQ для получения сообщений о событиях от кошелька.

**My private key** - Ваш приватный ключ (несжатый) для создания транзакции на Ваш адрес.

**Partner public key** - публичный ключ (несжатый) партнера для создания транзакции на адрес партнера.

**Amount** - количество монет (**в shatoshi**), которые Вы хотите потратить или получить.

**Confirmations** - количество подтверждений, которые нужны для того, чтобы можно было предполагать, что транзакции можно верить.

**Expire** - количество подтверждений, которые требуются для возврата монет обратно на адрес отправителя. Должно быть больше за значение **Confirmations** (*Убедитесь, что время, которое требуется для достижения данного количества подтверждений на Вашем блокчейне максимально приближенное до времени на блокчейне Вашего партнера*).

### Bitcoin настройки

Блок **Bitcoin settings** по своей сути является таким же, как и **Minexcoin settings** но для кашелька Bitcoin.

### Действие

Вы должны выбрать верное действие с монетами. Выберите одно из двух действий - **Sell Minexcoin**/**Buy Minexcoin** (**Продать Minexcoin**/**Купить Minexcoin**) в выпадающем списке.

### Запуск

1. Заполните все поля окна актуальными данными.
2. Выберете нужное действие из выпадающего списка.
3. Нажмите кнопку **Exchange**.
4. Следите за исполнением.