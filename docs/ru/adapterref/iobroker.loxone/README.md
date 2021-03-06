---
translatedFrom: en
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/adapterref/iobroker.loxone/README.md
title: ioBroker.loxone
hash: Vaxpp7GZIwtLcovK5YzPzm1NMAypZb4LvIzBmQxOWLk=
---
![Логотип](../../../en/adapterref/iobroker.loxone/admin/loxone.png)

![Версия NPM](http://img.shields.io/npm/v/iobroker.loxone.svg)
![Загрузки](https://img.shields.io/npm/dm/iobroker.loxone.svg)
![Количество установок (последнее)](http://iobroker.live/badges/loxone-installed.svg)
![Количество установок (стабильно)](http://iobroker.live/badges/loxone-stable.svg)
![Статус зависимости](https://img.shields.io/david/UncleSamSwiss/iobroker.loxone.svg)
![НПМ](https://nodei.co/npm/iobroker.loxone.png?downloads=true)
![Трэвис-Си](http://img.shields.io/travis/UncleSamSwiss/ioBroker.loxone/master.svg)

# IoBroker.loxone
[![Статус перевода] (https://weblate.iobroker.net/widgets/adapters/-/loxone/svg-badge.svg)](https://weblate.iobroker.net/engage/adapters/?utm_source=widget)

![Тестирование и выпуск](https://github.com/UncleSamSwiss/ioBroker.loxone/workflows/Test%20and%20Release/badge.svg)

## Адаптер loxone для ioBroker
** _ Для этого адаптера требуется как минимум nodejs 10.x! _ **

Извлекает всю информацию, доступную в Loxone Miniserver (и Loxone Miniserver Go), и предоставляет изменения в реальном времени.

## Установить
Установите этот адаптер через ioBroker Admin:

1. Откройте диалоговое окно конфигурации экземпляра.
2. Введите IP-адрес или имя хоста и HTTP-порт (по умолчанию 80) вашего Loxone Miniserver.
3. Создайте нового пользователя в Loxone Miniserver (с помощью приложения Loxone Config), которому вы даете права только на чтение и запись для всех необходимых переменных.
4. Введите имя этого пользователя и его пароль в диалоговом окне конфигурации.
5. Сохраните конфигурацию.
6. Запустите адаптер.

## Конфигурация
### Имя хоста / IP-адрес минисервера
Это IP-адрес или имя хоста вашего Loxone Miniserver или Miniserver Go.

### Порт минисервера
Это HTTP-порт вашего Loxone Miniserver.

По умолчанию Miniserver настроен на прослушивание порта 80, но вы могли его изменить.

### Имя пользователя Miniserver
Укажите действительное имя пользователя для доступа к Loxone Miniserver.

По соображениям безопасности настоятельно рекомендуется использовать пользователя, отличного от admin.

Пользователю нужен только доступ для чтения к переменным, которые вы хотите использовать из ioBroker.

### Пароль мини-сервера
Введите пароль для данного имени пользователя (см. Выше).

Имейте в виду, что этот пароль хранится в незащищенном виде внутри ioBroker - поэтому не используйте пользователя «admin»!

### Синхронизировать имена
Это обновит имена в ioBroker всякий раз, когда они изменятся в конфигурации Loxone.
Если этот параметр отключен, имена будут синхронизироваться только при первом обнаружении элемента управления.

### Синхронизировать комнаты
Это заполнит перечисление enum.rooms всеми комнатами, предоставленными Loxone Miniserver, и свяжет все элементы управления.

### Функции синхронизации
Это заполнит перечисление enum.functions всеми категориями, предоставляемыми Loxone Miniserver, и свяжет все элементы управления.

## Состояния
Адаптер автоматически подключается к настроенному мини-серверу Loxone и создает состояния для каждого обнаруженного состояния управления.

Идентификаторы состояний имеют следующий формат: `loxone.<instance>.<control>.<state>`

- `<instance>` - это индекс экземпляра адаптера ioBroker (обычно "0")
- <control> - это UUID элемента управления
- `<state>` - состояние в элементе управления (дополнительную информацию см. в разделе [Поддерживаемые типы элементов управления] (# supported-control-types)).

Имя, указанное при настройке элемента управления в Loxone Config, будет использоваться только как его отображаемое имя в ioBroker.
Это потому, что пользователь может выбрать одно и то же имя для нескольких элементов управления.

Для получения дополнительной информации об элементах управления и их состояниях также ознакомьтесь с API Loxone (особенно с файлом структуры): https://www.loxone.com/enen/kb/api/

## Контроль видимости
По умолчанию Loxone Miniserver скрывает многие элементы управления (и, следовательно, их состояния) от веб-интерфейса.

Это означает, что они также скрыты от этого адаптера ioBroker.

Чтобы гарантировать, что все ваши состояния должным образом передаются в ioBroker, убедитесь, что у них установлен флажок «Использовать в визуализации»:

![Использовать в настройках визуализации](../../../en/adapterref/iobroker.loxone/doc/loxone-config-use-in-visualization.png)

## Глобальные состояния
В настоящее время этот адаптер обеспечивает следующие глобальные состояния:

- «operatingMode»: номер текущего режима работы Loxone Miniserver.
- `operatingMode-text`: текущий режим работы Loxone Miniserver в виде текста
- «восход»: количество минут после полуночи, когда сегодня встает солнце.
- `sunset`: количество минут после полуночи, когда сегодня садится солнце
- `notifications`: количество уведомлений
- «модификации»: количество модификаций.
- все остальные глобальные состояния просто сообщаются как тексты

## Поддерживаемые типы управления
В настоящее время этот адаптер поддерживает следующие типы элементов управления.

За названием штата вы можете увидеть его тип:

- `(rw)`: доступно для чтения и записи: это состояние можно изменить из ioBroker
- `(ro)`: только для чтения: это состояние нельзя изменить из ioBroker
- `(wo)`: только для записи: значение этого состояния не сообщается этим адаптером, но его можно изменить, запустив какое-либо действие на Loxone Miniserver

### Тревога
Обеспечивается охранной сигнализацией.

- логическое состояние (истина / ложь) тревоги «активирован» (rw); запись в это значение true немедленно включит тревогу (без заранее заданной задержки)
- `nextLevel` (ro) идентификатор следующего уровня тревоги
    - 1 = Без звука
    - 2 = Акустический
    - 3 = оптический
    - 4 = внутренний
    - 5 = Внешний
    - 6 = Удаленный
- `nextLevelDelay` (ro) задержка следующего уровня в секундах
- `nextLevelDelayTotal` (ro) общая задержка следующего уровня в секундах
- `level` (ro) идентификатор текущего уровня тревоги
    - 1 = Без звука
    - 2 = Акустический
    - 3 = оптический
    - 4 = внутренний
    - 5 = Внешний
    - 6 = Удаленный
- `startTime` (ro) отметка времени начала тревоги
- `weaponDelay` (ro) задержка постановки управления тревогой
- `weaponDelayTotal` (ro) общая задержка постановки управления тревогой
- `сенсоры` (ro) список сенсоров
- `disabledMove` (rw) движение отключено (true) или нет (false)
- `delayedOn` (wo) запись любого значения в это состояние включает сигнализацию с настроенной задержкой
- `quit` (wo) запись любого значения в это состояние подтверждает тревогу

### Центральная сигнализация
Обеспечивается центральной охранной сигнализацией.

- логическое состояние (истина / ложь) тревоги «активирован» (rw); запись в это значение true немедленно включит тревогу (без заранее заданной задержки)
- `delayedOn` (wo) запись любого значения в это состояние включает сигнализацию с настроенной задержкой
- `quit` (wo) запись любого значения в это состояние подтверждает тревогу

### Будильник
Предусмотрено управление будильником.

- `isEnabled` (rw) логическое состояние (истина / ложь) будильника
- `isAlarmActive` (ro) логическое (истина / ложь), звонит ли в настоящее время будильник
- `confirmNeeded` (ro) логическое (true / false), нужно ли пользователю подтверждать тревогу
- `ringingTime` (ro) обратный отсчет в секундах, как долго будильник будет звонить, пока он снова не повторится
- ringDuration (rw) продолжительность звонка будильника в секундах
- Время подготовки `prepareDuration` (rw) в секундах
- `snoozeTime` (ro) секунд до окончания повтора
- `snoozeDuration` (rw) продолжительность откладывания в секундах
- `snooze` (wo) запись любого значения в это состояние откладывает текущий будильник
- `dismiss` (wo) запись любого значения в это состояние отклоняет текущий сигнал тревоги

### AudioZone
Предоставлено Music Server Zone.

- состояние музыкального сервера `serverState` (ro):
    - -3 = неизвестная / недопустимая зона
    - -2 = недоступен
    - -1 = неизвестно
    - 0 = не в сети
    - 1 = инициализация (загрузка, попытка доступа)
    - 2 = онлайн
- `playState` (rw) состояние воспроизведения:
    - -1 = неизвестно (это значение не может быть установлено)
    - 0 = остановлено (установка этого значения приостановит воспроизведение)
    - 1 = пауза (установка этого значения приостановит воспроизведение)
    - 2 = воспроизведение (установка этого значения запускает / возобновляет воспроизведение)
- состояние клиента `clientState` (ro):
    - 0 = не в сети
    - 1 = инициализация (загрузка, попытка доступа)
    - 2 = онлайн
- `power` (rw) независимо от того, активна ли мощность клиента
- `volume` (rw) текущий объем
- зонам maxVolume (ro) можно назначить максимальную громкость
- `shuffle` (rw), включено ли перемешивание списка воспроизведения
- `sourceList` (ro) список, содержащий все избранные зоны
- режим повтора `repeat` (rw):
    - -1 = неизвестно
    - 0 = выкл.
    - 1 = повторить все
    - 2 = -не используется-
    - 3 = повторить текущий элемент
- `songName` (ro) название песни
- `duration` (ro) длина всего трека, -1, если не известно (поток)
- `progress` (rw) текущая позиция в треке
- `album` (ro) название альбома
- `artist` (ro) имя исполнителя
- `station` (ro) название станции
- `жанр` (ro) название жанра
- URL изображения обложки песни или альбома `cover` (ro)
- `source` (rw) текущий выбранный идентификатор источника (см.` sourceList` выше)
- `prev` (wo) запись любого значения в это состояние переходит на предыдущую дорожку
- `next` (wo) запись любого значения в это состояние переходит к следующему треку

### Central Audio
Предоставляется центральным музыкальным сервером.

- `control` (wo) устанавливает состояние игры для всех игроков (` true` = играть, `false` = пауза)

### Colorpicker
Это устройство появляется только внутри LightController.

- `red` (rw) красный значение палитры цветов
- `green` (rw) зеленый значение палитры цветов
- `blue` (rw) синий значение палитры цветов

Установка одного или нескольких из указанных выше состояний из ioBroker отправит команду в Miniserver только примерно через 100 мс.
Это сделано для предотвращения многократного изменения цвета при вводе одного пользователя.

### Colorpicker V2
Это устройство появляется только в Light Controller V2 в программном обеспечении Loxone версии 9 и выше.

- `red` (rw) красный значение палитры цветов
- `green` (rw) зеленый значение палитры цветов
- `blue` (rw) синий значение палитры цветов

Установка одного или нескольких из указанных выше состояний из ioBroker отправит команду в Miniserver только примерно через 100 мс.
Это сделано для предотвращения многократного изменения цвета при вводе одного пользователя.

### Диммер
Обеспечивается диммерами.

- `position` (rw) текущее положение диммера
- `min` (ro) текущее минимальное значение
- `max` (ro) текущее максимальное значение
- `step` (ro) текущее значение шага
- `on` (wo) запись любого значения в это состояние устанавливает диммер в последнее известное положение
- `off` (wo) запись любого значения в это состояние отключает диммер, устанавливает позицию в 0, но запоминает последнюю позицию

### Ворота
Обеспечивается управлением воротами.

- `position` (ro) позиция от 1 = вверх до 0 = вниз
- `active` (rw) текущее направление движения ворот
    - -1 = закрыть
    - 0 = не движется
    - 1 = открыто
- `preventOpen` (ro) предотвращает ли открытие двери
- `preventClose` (ro) предотвращает ли закрытие двери

### Центральные ворота
Обеспечивается центральным управлением воротами.

- `open` (wo) открывает все ворота
- `close` (wo) закрывает все ворота
- `stop` (wo) останавливает все двигатели ворот

### InfoOnlyDigital
Предоставляется виртуальными состояниями, а также переключателем Loxone Touch.

- `active` (ro) логическое состояние (true / false) элемента управления
- `active-text` (ro), если настроено, текстовый эквивалент состояния
- `active-image` (ro), если настроено, изображение, эквивалентное состоянию
- `active-color` (ro), если настроено, цветовой эквивалент состояния

![InfoOnlyDigital настройки](../../../en/adapterref/iobroker.loxone/doc/loxone-config-info-only-digital.png)

### InfoOnlyAnalog
Предоставляется виртуальными состояниями, а также переключателем Loxone Touch.

- `value` (ro) значение состояния (номер) элемента управления
- `value-formatted` (ro), если настроено, форматированное значение состояния (с использованием формата« Unit »из Loxone Config)

### Внутренняя связь
Предоставляется дверными контроллерами.

- `bell` (ro) звонит ли колокол
- Массив `lastBellEvents` (ro), содержащий временные метки для каждого звонка, на который не ответили
- `version` (ro) Только для домофонов Loxone - текст, содержащий текущую установленную прошивку

    версии

- `answer` (wo) запись любого значения в это состояние отключит звонок

Этот тип канала может содержать другие устройства. См. Дополнительную информацию в соответствующей главе.

### Жалюзи
Предусмотрены различные виды жалюзи (автоматические и ручные).

- `up` (rw) поднимается ли Жалюзи вверх
- `down` (rw), движется ли Жалюзи вниз
- `position` (ro) позиция жалюзи, число от 0 до 1
    - Верхнее положение жалюзи = 0
    - нижнее положение жалюзи = 1
- `shadePosition` (ro) положение тени жалюзи (жалюзи), число от 0 до 1
    - Жалюзи не заштрихованы = 0
    - Жалюзи заштрихованы = 1
- «SafetyActive» (ro) используется только теми, у кого есть автопилот, это означает аварийное отключение
- `autoAllowed` (ro) используется только теми, у кого есть автопилот
- `autoActive` (rw) используется только теми, у кого есть автопилот
- `заблокировано` (ro) только теми, у кого есть автопилот, это представляет собой выходной QI в Loxone Config
- `infoText` (ro) сообщает, например, от того, что вызвало заблокированное состояние или что привело к срабатыванию защиты.
- `fullUp` (wo) запись любого значения в это состояние вызывает полное движение вверх
- `fullDown` (wo) запись любого значения в это состояние вызывает полное движение вниз
- `shade` (wo), записав любое значение в это состояние, затеняет жалюзи в идеальное положение

### Центральные жалюзи
Обеспечивается центральным управлением жалюзи.

- `autoActive` (rw) используется только теми, у кого есть автопилот
- `fullUp` (wo) запись любого значения в это состояние вызывает полное движение вверх
- `fullDown` (wo) запись любого значения в это состояние вызывает полное движение вниз
- `shade` (wo) записывает любое значение в это состояние, затемняет все жалюзи в идеальное положение

### Световой контроллер
Предоставляется контроллерами освещения (отеля).
Сцены можно изменять только в приложениях Loxone, но их можно выбрать в ioBroker.

- `activeScene` (rw) номер текущей активной сцены
    - 0: все выключено
    - 1..8: сцена, определяемая пользователем (определение / изучение сцен должно выполняться с помощью инструментов Loxone)
    - 9: все включено
- `sceneList` (ro) список всех сцен
- `plus` (wo) переходит к следующей сцене
- `minus` (wo) заменяет предыдущую сцену

Этот тип канала может содержать другие устройства. См. Дополнительную информацию в соответствующей главе.

### Световой контроллер V2
Предоставляется контроллерами освещения (отеля) в программном обеспечении Loxone версии 9 и выше.
Настроения можно изменять только в приложениях Loxone, но их можно выбирать и комбинировать в ioBroker.

- `moodList` (ro) список всех настроенных имен настроений
- `activeMoods` (rw) текущий активный список названий настроений
- `favouriteMoods` (ro) список любимых названий настроения
- `additionalMoods` (ro) список не любимых названий настроений
- `plus` (wo) переходит к следующему настроению
- `minus` (wo) изменяет предыдущее настроение

Этот тип канала может содержать другие устройства. См. Дополнительную информацию в соответствующей главе.

### Центральный контроллер света
Обеспечивается центральным контроллером освещения.

- `control` (wo) включает или выключает все огни

### Метр
Обеспечено счетчиками коммунальных услуг.

- `actual` (ro) фактическое значение (число)
- `actual-formatted` (ro), если настроено, отформатированное фактическое значение состояния (с использованием формата" Unit "из Loxone Config)
- `total` (ro) общая стоимость (число)
- `total-formatted` (ro), если настроено, отформатированное общее значение состояния (с использованием формата" Unit "из Loxone Config)
- `reset` (wo) запись любого значения в это состояние сбрасывает общее значение

### Нажать кнопку
Обеспечивается виртуальными кнопочными вводами.

- `active` (rw) текущее состояние кнопки
- `pulse` (wo) запись любого значения в это состояние будет имитировать нажатие кнопки только на очень короткое время

### Слайдер
Обеспечивается аналоговыми виртуальными входами.

- `value` (rw) текущее значение ползунка
- `value-formatted` (ro), если настроено, форматированное значение состояния (с использованием формата« Unit »из Loxone Config)
- `error` (ro) указывает на недопустимое значение ползунка

### Дымовая сигнализация
Обеспечено счетчиками коммунальных услуг.

- `nextLevel` (ro) идентификатор следующего уровня тревоги
    - 1 = Без звука
    - 2 = Акустический
    - 3 = оптический
    - 4 = внутренний
    - 5 = Внешний
    - 6 = Удаленный
- `nextLevelDelay` (ro) задержка следующего уровня в секундах
- `nextLevelDelayTotal` (ro) общая задержка следующего уровня в секундах
- `level` (ro) идентификатор текущего уровня тревоги
    - 1 = Без звука
    - 2 = Акустический
    - 3 = оптический
    - 4 = внутренний
    - 5 = Внешний
    - 6 = Удаленный
- `сенсоры` (ro) список сенсоров
- состояние акустической тревоги «ousticAlarm »(ro) ложное для неактивного и истинное для активного
- `testAlarm` (ro) активен ли testalarm
- «alarmCause» (ro) причина срабатывания сигнализации:
    - 1 = только датчик дыма
    - 2 = только вода
    - 3 = дым и вода
    - 4 = только температура
    - 5 = огонь и температура
    - 6 = температура и вода
    - 7 = огонь, температура и вода
- `startTime` (ro) отметка времени при запуске будильника
- `timeServiceMode` (rw) задержка до отключения сервисного режима
- `mute` (wo) запись любого значения в это состояние отключает сирену
- `quit` (wo) запись любого значения в это состояние подтверждает срабатывание дымовой сигнализации

### Переключатель
Предоставляется виртуальными входными переключателями.

- `active` (rw) текущее состояние переключателя

### TimedSwitch
Предусмотрено лестничными клетками и многофункциональными переключателями.

- `deactivationDelayTotal` (ro) секунд, как долго выход будет активен, если используется таймер
- обратный отсчет `deactivationDelay` (ro) до отключения выхода
    - 0 = выход выключен
    - -1 = выход постоянно включен
    - иначе будет отсчет от деактивацииDelayTotal
- `active` (wo) включает или выключает переключатель (без задержки деактивации)
- `pulse` (wo) импульсный переключатель:
    - deactivationDelay = 0
        - Запустит обратный отсчет, от deactivationDelayTotal до 0
    - если это переключатель подъезда:
        - deactivationDelay = -1
            - Нет эффекта, останется постоянно включенным.
        - deactivationDelay> 0
            - перезапускает обратный отсчет
    - если это многофункциональный переключатель
        - выключает (из обратного отсчета или постоянного состояния)

### Трекер
Предусмотрено лестничными клетками и многофункциональными переключателями.

- `entry` (ro) список записей, возвращаемых минисервером

### WindowMonitor
Обеспечено счетчиками коммунальных услуг.

- `numOpen` (ro) количество открытых окон и дверей
- `numClosed` (ro) количество закрытых окон и дверей
- `numTilted` (ro) количество наклонных окон и дверей
- `numOffline` (ro) количество окон и дверей, которые недоступны
- `numLocked` (ro) количество запертых окон и дверей
- `numUnlocked` (ro) количество открытых окон и дверей

Сумма значений из всех этих состояний равна количеству контролируемых окон и дверей. Окна / двери с двумя состояниями всегда будут считаться "худшим" состоянием.

Для каждого контролируемого окна / двери будет устройство с индексом в качестве идентификатора и заданным именем. У них есть следующие состояния:

- `closed` (ro) окно / дверь закрыто
- `tilted` (ro) окно / дверь наклонено
- `open` (ro) окно / дверь открыто
- `locked` (ro) окно / дверь заблокированы
- `unlocked` (ro) окно / дверь разблокировано

## Сервер погоды
Информация о погодном сервере предоставляется в виде устройства с несколькими каналами.
Устройство называется `WeatherServer`.
Это содержит:

- канал `Актуально` с текущими значениями погоды
- один канал на каждый прогнозируемый час под названием `HourXX`, где` XX` - количество часов с текущего момента

Каждый канал содержит следующие состояния:

- barometricPressure: числовое значение атмосферного давления.
- `barometricPressure-formatted`: значение атмосферного давления в формате с указанием единиц
- `dewPoint`: числовое значение точки росы
- `dewPoint-formatted`: форматированное значение точки росы с единицей измерения
- «воспринимаемая температура»: числовое значение воспринимаемой температуры.
- `воспринимаемая температура-форматированная`: форматированное значение воспринимаемой температуры с единицей измерения
- «осадки»: числовое значение осадков.
- «осадка в формате»: значение осадков в формате с единицей измерения.
- «relativeHumidity»: числовое значение относительной влажности.
- `relativeHumidity-formatted`: форматированное значение относительной влажности с единицей измерения
- `solarRadiation`: значение солнечной радиации.
- `temperature`: числовое значение температуры
- `temperature-formatted`: значение температуры в формате с указанием единиц
- `timestamp`: отметка времени данных как` value.time` (время JavaScript)
- `weatherType`: числовое значение перечисления типа погоды
- `weatherType-text`: текстовое представление типа погоды
- windDirection: значение направления ветра
- windSpeed: значение скорости ветра
- `windSpeed-formatted`: значение скорости ветра в формате с единицей измерения

## Совместимость
Совместимость была протестирована с Loxone Miniserver Go 9.0.9.26 с использованием Loxone Config 9.0.9.26.

## Отчеты об ошибках и запросы функций
Пожалуйста, используйте репозиторий GitHub, чтобы сообщать об ошибках или запрашивать новые функции.

Если вам требуется отсутствующий тип элемента управления, укажите имя, как оно записано в журнале ошибок ioBroker, а также все необработанное содержимое устройства в дереве объектов ioBroker:

Пример файла журнала для "LightController":

![Журнал отсутствующего элемента управления LightController](../../../en/adapterref/iobroker.loxone/doc/log-missing-control-type.png)

Собственное значение от ioBroker &gt; Объекты

![Подробная информация об отсутствующем элементе управления LightController](../../../en/adapterref/iobroker.loxone/doc/details-missing-control-type.png)

## Legal
Этот проект не связан прямо или косвенно с компанией Loxone Electronics GmbH.

Loxone и Miniserver являются зарегистрированными товарными знаками Loxone Electronics GmbH.

## Changelog

### 2.0.1 (2020-09-24)

-   (UncleSamSwiss) Fixed percentage states always showing 0% (#49)
-   (UncleSamSwiss) Fixed analog virtual inputs wouldn't set the value 0 from ioBroker (#47)
-   (UncleSamSwiss) Added translations to package information.

### 2.0.0

-   (UncleSamSwiss) Updated to the latest development tools and changed to the TypeScript language

### 1.1.0

-   (UncleSamSwiss) Added support for Miniserver Gen 2
-   (sstroot) RGB for LightControllerV2
-   (Apollon77) Updated CI Testing

### 1.0.0

-   (UncleSamSwiss) Fixed issue that was resetting the custom settings and cloud smartName
-   (alladdin) Fixed connection issues with Loxone Miniserver 10
-   (UncleSamSwiss) Changed all write-only "switch"es to "button"s
-   (UncleSamSwiss) Added support for AlarmClock control
-   (Apollon77) Updated CI Testing

### 0.4.0

-   (UncleSamSwiss) Improved support for Loxone Config 9
-   (UncleSamSwiss) Changed all color choosers (i.e. color lights) to use RGB (previously HSV/HSL was completely wrong)

### 0.3.0

-   (UncleSamSwiss) Control names only synchronized on the first time by default (configurable); users can change control names the way they want

### 0.2.1

-   (UncleSamSwiss) Added support for Slider control

### 0.2.0

-   (UncleSamSwiss) Added proper support for Alexa for the following controls: Alarm, AudioZone, Gate, Jalousie and LightController

### 0.1.1

-   (UncleSamSwiss) Added support for synchronizing rooms and functions (categories) from Loxone Miniserver

### 0.1.0

-   (UncleSamSwiss) Added support for many more controls including commands from ioBroker to Loxone Miniserver

### 0.0.3

-   (Bluefox) Formatting, refactoring and Russian translations

### 0.0.2

-   (UncleSamSwiss) Added creation of an empty device for all unsupported controls (helps figure out its configuration)

### 0.0.1

-   (UncleSamSwiss) Initial version

## License

Copyright 2020 UncleSamSwiss

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.