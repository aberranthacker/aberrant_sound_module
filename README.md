# Aberrant Sound Module

## О устройстве.
Звуковая карта на базе AY-3-8912 для микрокомпьютера "[Электроника МС 0511](https://ru.wikipedia.org/wiki/%D0%AD%D0%BB%D0%B5%D0%BA%D1%82%D1%80%D0%BE%D0%BD%D0%B8%D0%BA%D0%B0_%D0%9C%D0%A1_0511)" (УКНЦ).
![photo-of-the-module](Doc/IMG_5550.JPG)

## Участники проекта
* Схема - [aberranthacker](https://github.com/aberranthacker)
* Финальная ревизия схемы и трассировка печатной платы - [zloiMOZG](https://github.com/zloiMOZG)

## Особенности
* 3 звукогенератора AY-3-8912
* шинные драйверы с инверсией, прощай программное инвертирование :)
* разъем расширения P2, позволяет подключать к ПП дополнительные устройства без
  дублирования логики работы с шиной и дешифрации адреса
* диапазон адресов 0177360-0177377
  * адреса 0177360, 0177362 и 0177364 используются AY-3-8912
  * линии детектора адреса диапазона 0177366-0177377 выведены на future
    connector (P2)
* всё на мелкой логике, в "ламповых" DIP корпусах
* обмен со звукогенераторами реализован так же как на компьютерах серии БК
  * записью слова, передаётся адрес регистра AY
  * записью байта, передаются данные в регистр звукогенератора

## А есть ли софт?!
На данный момент, вывод звука работает в игре [ChibiAkuma's](https://github.com/aberranthacker/chibiakumas), и в музыкальном демо [timeCS](https://github.com/aberranthacker/timeCS).

Портирован [The AKG (generic) player](https://github.com/aberranthacker/akg_player). Для музыки созданной, в пожалуй самом навороченном [Arkos Tracker 2](http://www.julien-nevo.com/arkostracker/). Так же в нём можно создавать звуковые эффекты, не особенно вникая в спицифику работы с AY.

Плюс, [адаптирована](https://github.com/aberranthacker/timeCS/blob/master/pt3play2.s) БК-0011М версия проигрывателя `*.pt3`.
Особенностью УКНЦ версии является то, что она рассчитана на работу с треком в
одном из банков памяти. Т.е. считывание трека идёт побайтово, из определённого
банка памяти, используя регистры адреса/данных. В случае использования банков 1
или 2, а так же, если есть готовность допустить затирание ОЗУ ЦП режима HALT, то это
позволяет проигрывать треки размером до 36К на чип.

## Хочу заказать плату, но где #%$^@ герберы?!
`./Project Outputs for aberrant_sound_module/aberrant_sound_module 1.0.0/`

## Соображения
Звуковые возможности УКНЦ ограниченны 1-битной пищалкой. И к сожалению они не были
расширены в те времена, когда трава была зеленее, а эти компьютеры выпускались и массово использовались.

Идея создания звуковой карты вынашивалась давно, но только в процессе
портирования игры [ChibiAkuma's](https://github.com/aberranthacker/chibiakumas) возникла потребность в подобном устройстве.
Потребность, оформившая видение каким оно должно быть:
* аутентичное устройство, собранное на компонентах доступных в начале 90-х.
Практически вольная фантазия на тему того, каким бы оно могло быть, получи УКНЦ большее
распространение, в качестве бытового компьютера.
* Размер, не больше размера КГМД.
* Наличие future connector'а (P2). Для максимально упрощённого подключение
  дополнительных устройств к переферийному процессору.
  Изначально была задумка подключить к этому разъёму YM3812(OPL2),
  пару ЦАП КР572ПА1(AD7520), и RAM диск. Но на данный момент дополнительные
  модули не реализованны.
