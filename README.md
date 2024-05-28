# Aberrant Sound Module
The English version of the description can be found [down below](#english-version-of-the-descripion).

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

## Недостатки текущей ревизии платы
* вырез под ключ в нижней части платы, не совпадает с ключём слота ПП, вырез необходимо расширить влево, на половину его ширины
* футпринт кварцевого генератора выполнен зеркально, генератор необходимо развернуть на 180 градусов и пробросить перемычку

## А есть ли софт?
На данный момент, вывод звука работает в игре [ChibiAkuma's](https://github.com/aberranthacker/chibiakumas), и в музыкальном демо [timeCS](https://github.com/aberranthacker/timeCS).

Портирован [The AKG (generic) player](https://github.com/aberranthacker/akg_player). Для музыки созданной, в пожалуй самом навороченном [Arkos Tracker 2](http://www.julien-nevo.com/arkostracker/). Так же в нём можно создавать звуковые эффекты, не особенно вникая в специфику работы с AY.

Плюс, [адаптирована](https://github.com/aberranthacker/timeCS/blob/master/pt3play2.s) БК-0011М версия проигрывателя `*.pt3`.
Особенностью УКНЦ версии является то, что она рассчитана на работу с треком в
одном из банков памяти. Т.е. считывание трека идёт побайтово, из определённого
банка памяти, используя регистры адреса/данных. В случае использования банков 1
или 2 (а так же, если есть готовность допустить затирание ОЗУ ЦП режима HALT), это
предоставляет возможность проигрывать треки размером до 36К на чип.

## Хочу заказать плату, а где герберы?
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

# English version of the descripion
## About the Device
A sound card based on the AY-3-8912 for the "Elektronika MS 0511" (UKNC) microcomputer.
![photo-of-the-module](Doc/IMG_5550.JPG)

## Project Participants

* Schematic: [aberranthacker](https://github.com/aberranthacker)
* Final schematic revision and PCB layout: [zloiMOZG](https://github.com/zloiMOZG)

## Features
* 3 x AY-3-8912 sound generators
* Bus drivers with inversion, no more software inversion :)
* P2 expansion connector, allows connecting additional devices to the PCB without duplicating bus logic and address decoding
* Address range 0177360-0177377
  * Addresses 0177360, 0177362, and 0177364 are used by the AY-3-8912
  * Address detector lines for the range 0177366-0177377 are routed to the future connector (P2)
* All built with SSI chips in "retro" DIP packages, giving it a warm, nostalgic feel
* Interaction with the sound generators is implemented similarly to the BK series computers:
  * Writing a word transmits the AY register address
  * Writing a byte transmits data to the sound generator register

## Drawbacks of the Current PCB Revision
* The cutout for the key in the lower part of the board does not match the slot key, it needs to be expanded to the left by half its width
* The footprint of the crystal oscillator is mirrored, the oscillator needs to be rotated 180 degrees and a jumper wire added

## Is there any software?
Currently, sound output works in the game ChibiAkuma's and in the music demo timeCS.

The AKG (generic) player has been ported.
It can play music created in the sophisticated Arkos Tracker 2.
Additionally, sound effects can be created without delving deeply into the specifics of working with AY.

Moreover, the BK-0011M version of the `*.pt3` player [has been adapted](https://github.com/aberranthacker/timeCS/blob/master/pt3play2.s).
The UKNC version is designed to work with a track in one of the memory banks.
That is, the track is read byte by byte from a specific memory bank using address/data registers.
Using banks 1 or 2 (and if you are willing to overwrite the CPU's HALT mode RAM),
it is possible to play tracks up to 36K in size on the chip.

## Where are the gerbers to order the board?
`./Project Outputs for aberrant_sound_module/aberrant_sound_module 1.0.0/`

## Considerations
The sound capabilities of the UKNC are limited to a 1-bit beeper.
Unfortunately, they were not expanded during the time when these computers were being produced and widely used.

The idea of creating a sound card had been considered for a long time, but the need for such a device became apparent during the process of porting the game ChibiAkuma's.
This need shaped the vision of what it should be:
* An authentic device built with components available in the early '90s.
  Essentially a free fantasy on what it could have been had the UKNC seen greater adoption as a home computer.
* Size no larger than the FDC module.
* Inclusion of a future connector (P2) for simplified connection of additional devices to the peripheral processor.
  Initially, there was an idea to connect a YM3812 (OPL2), a couple of KR572PA1 (AD7520) DACs, and a RAM disk to this connector.
  However, these additional modules have not been implemented yet.
