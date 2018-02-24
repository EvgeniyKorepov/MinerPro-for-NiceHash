# MinerPro for NiceHash
NiceHash Miner Pro

([English version](README.md))

- [Особенности](#features)
- [Как подготовить Excavator?](#PrepareExcavator)
- [Как пользоваться MinerPro for NiceHash?](#HowtoUseMinerProforNiceHash)

<img src="Resources/screenshot008.PNG" />

# <a name="features"></a> Особенности
- Расчет прибыли производится с учетом стоимости электроэнергии. Включая различную стоимость электричества в течение дня.
- Индивидуальный разгон GPU для каждого алгоритма.
- Точная настройка параметров алгоритмов.
- Возможность изменения параметров разгона во время работы.
- Быстро, менее одной секунды, переключаться между алгоритмами.
- Отказоустойчивость - переход на другие локации при сбое stratum-сервера.
- Кэширование данных SMA Nicehash.
- Поддерживаемая валюта USD, CHF, HRK, MXN, ZAR, INR, CNY, THB, AUD, ILS, KRW, JPY, PLN, GBP, IDR, HUF, PHP, TRY, RUB, HKD, ISK, EUR, DKK, CAD , MYR, BGN, NOK, RON, SGD, CZK, SEK, NZD, BRL.
- Интеграция с андроид-приложением Nicehash Statistics (https://play.google.com/store/apps/details?id=ru.flintnet.NiceHashStat). Теперь вы получите push-уведомления об остановке буровых установок. Также в мобильном приложении вы можете посмотреть логи MinerPro
- Dev 0,8% вознаграждение разработчику (одна минута каждые два часа).

# <a name="PrepareExcavator"></a> Как подготовить Excavator?

1. Скачайте Excavator с официального источника [https://github.com/nicehash/excavator](https://github.com/nicehash/excavator) и распакуйте в удобную для вас Папку.
2. Создайте файл конфигурации [ExcavatorServer.json](https://github.com/EvgeniyKorepov/MinerPro-for-NiceHash/blob/master/ExcavatorServer.json) в папке с Экскаватором. Не забудьте изменить его в соответствии с количеством ваших GPU:
```json
[
  {"time":15,"loop":15,"commands":[{"id":1,"method":"algorithm.print.speeds","params":[]}]},
  {"event":"on_quit","commands":[{"id":1,"method":"device.set.tdp","params":["0","100"]},
  {"id":1,"method":"device.set.core_delta","params":["0","0"]},
  {"id":1,"method":"device.set.memory_delta","params":["0","0"]}]}
]
 ```
3. Создайте запускаемый файл [#start.cmd](https://github.com/EvgeniyKorepov/MinerPro-for-NiceHash/blob/master/%23start.cmd) в папке Экскаватора 
```
@echo off
:: CONFIG STARTS
SET LOCALDIR=%~dp0
SET CONSOLE_LOG_LEVEL=2
SET FILE_LOG_LEVEL=0
SET WEB_PORT=38080
SET WEB_HOST=0.0.0.0
SET TOKEN=olaniel666
SET PORT=33333
SET HOST=0.0.0.0
SET RESTART_DELAY=0
SET RESTART_DELAY_LONG=30
:: CONFIG ENDS
cd /d "%LOCALDIR%"
:start
SET COMMAND_FILE=ExcavatorServer.json
excavator.exe -c %LOCALDIR%%COMMAND_FILE% -d %CONSOLE_LOG_LEVEL% -f %FILE_LOG_LEVEL% -wp %WEB_PORT% -wi %WEB_HOST% -wa %TOKEN% -p %PORT% -i %HOST%  
goto start
```
4. Запустите файл #start.cmd. Запускать его можете вручную или любимым способом автозапуска - Автозагрузка, Планировщик задач, и т.д..

# <a name="HowtoUseMinerProforNiceHash"></a> Как пользоваться MinerPro for NiceHash?

 [Короткое видео с демонстрацией первоначальной настройки и запуском](https://youtu.be/zN5rWmuU2mc)
 
1. [Подготовьте Экскаватор](#PrepareExcavator)
2. Скачайте последний релиз MinerPro https://github.com/EvgeniyKorepov/MinerPro-for-NiceHash/releases, распакуйте в удобную папку и запустите MinerProForNicehash.exe
3. При первом запуске вы попадете на страницу настроек - выберите валюту и нажмите Save. 
4. Откроется основной раздел приложения. В левой части, в Списке ригов, внизу, нажмите кнопку "Add Rig".
5. Вы попадете в раздел добавления ригов. Здесь вам нужно пройти три этапа настройки:
  - Выберите имя Рига (оно же будет именем воркера в Nicehash), введите свой Bitcoin адрес, Автозапуск автоматической добычи, предпочитаемую локации и резервные локации, в таблице стоимости электроэнергии введите стоимость согласно вашему тарифу на электричество в выбранной ранее в настройках валюте. Нажмите Save.
  - Выберите предпочитаемый метод доступа к API Экскаватора (HTTP или TCP), хост экскаватора (127.0.0.1 если локально или IP адрес компьютера если удаленно). При выборе HTTP вы можете указать секретный токен доступа (тот же что и в запускаемом файле Экскаватора). Нажмите Save.
  - Если все указано правильно, произойдет соединение с Экскаватором и вы увидете список доступных для майнинга GPU. Отметьте те GPU, которые хотите добавить в Риг. Добавить в Риг можно тольно однотипные GPU, если на фашей ферме несколько типов GPU, то нужно создать отдельный Риг для каждого типа. Нажмите Save, вы попадете в Основной раздел приложения.
6. Продолжение в процессе написания....
