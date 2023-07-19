# Aberrant Sound Module

## О устройстве.
Звуковая карта на базе AY-3-8912 для микрокомпьютера "Электроника МС 0511"
(УКНЦ).
![photo-of-the-module](Doc/IMG_5550.JPG)

## Особенности
* 3 звукогенератора AY-3-8912
* шинный драйверы с инверсией, прощай программное инвертирование :)
* разъем расширения P2, позволяет создавать дополнительные устройства без
  дублирования логики работы с шиной и дешифрации адреса
* диапазон адресов 0177360-0177377
  * адреса 0177360, 0177362 и 0177364 используются AY-3-8912
  * диапазон 0177366-0177377 зарезервирован под платы расширения
* всё на мелкой логике, в "ламповых" DIP корпусах
* обмен с звукогенераторами реализован так же как на компьютерах серии БК
  * записью слова передаем адрес регистра AY
  * записью байта, пишем в регистр звукогенератора

## А есть ли софт?!
На данный момент, вывод звука работает в игре [ChibiAkuma's](https://github.com/aberranthacker/chibiakumas) и в демо [timeCS](https://github.com/aberranthacker/timeCS).

Портирован [The AKG (generic) player](https://github.com/aberranthacker/akg_player) для музыки созданной, в пожалуй самом навороченном [Arkos Tracker 2](http://www.julien-nevo.com/arkostracker/).

Так же [адаптирована](https://github.com/aberranthacker/timeCS/blob/master/pt3play2.s) БК-0011М версия проигрывателя PT3.
Особенностью УКНЦ версии является то что она рассчитана на работу с треком в
одном из банков памяти. Т.е. считывание трека идёт побайтово, из определённого
банка памяти используя регистры адреса/данных. В случае использования банков 1
или 2, а так же если мы готовы допустить затирание ОЗУ ЦП режима HALT, то это
позволяет проигрывать треки размером до 36К на чип.

## Соображения
Звуковые возможности УКНЦ ограниченны 1-битной пищалкой, и к сожалению не были
расширенны во времена когда эти компьютеры выпускались и использовались.

Идея создания звуковой карты вынашивалась давно, но только в процессе переноса
игры [ChibiAkuma's](https://github.com/aberranthacker/chibiakumas)
возникла потребность в подобном устройстве, и в итоге сформировалось видение
каким оно должно быть:
* аутентичное устройство, собранное на компонентах доступных в начале 90-х.
Вольная фантазия на тему того, что могло быть сделано, получи УКНЦ большее
распространение в качестве бытового компьютера.
* Размер не больше размера КГМД.

Использование мелкой логики в связке небольшим размером печатной платы сильно
ограничивает сложность устройства.
С одной стороны это плюс - сложнее сделать что-то не соответствующее эпохе
данного компьютера.
А с другой минус, ведь имеется всего два слота расширения, и один из
них уже занят КГМД.

Поэтому на плату модуля был добавлен разъём расширения.
В будущем предполагается подцепить к нему, с обоих сторон модуля по
плате.
На одной будет пара YM3812(OPL2), и пара ЦАП КР572ПА1(AD7520)
На второй RAM диск.
