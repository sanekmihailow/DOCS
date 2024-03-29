### Links

[ipmnet.ru](http://ipmnet.ru/~sadilina/Fedora/303.html)

[win-linux.ru](http://win-linux.ru/parametry-jadra-linux/)

[wiki.archlinux.org](https://wiki.archlinux.org/index.php/kernel_parameters)

### передача параметров

1)Происходит через
* `Grub(загрузчик)`
  * `/boot/grub/menu.lst` Постоянные изменения для конкретной версии ядра (с точкой)
  
  Пример 
   ```nginx
  radeon.si_support=0 amdgpu.si_support=1 
  ```
  * `/etc/default/grub` - постоянные изменения 
  * `при загрузкуе` Удерживать <kbd> shift </kbd> Нажать <kbd> e </kbd> чтобы добавить параметры в конец строки с `linux` , ориентир обычно `quiet`
 
2)Происходит через
* `modrobe(загрузка модулей и их блокировка)`
  * `/etc/modprobe.d/` создать файл и вписывать параметры (без точки)
  
  Пример 
  ```nginx 
  options radeon si_support=0
  options amdgpu cik_support=1 
  ```
  
### проверка с какими параметрами собрано ядро

```nginx
1) zcat /proc/config.gz
2) если нет, то где-то в "/boot" (/boot/config-4.9.12-040912-generic)
3) cat /proc/cmdline
```

### Основые параметры

| ***command*** | ***Description*** |
|---|---|
| <b>apci=off</b>          | Полностью отключает ACPI (Advanced Configuration and Power Interface). Полезен на некоторых ноутбуках,                                  когда не удается установить (а потом загрузкить) Linux. |
| <b>boot_delay=N</b>      | С помощью этого параметра вы можете установить задержку в N секунд перед выводом следующего сообщения                                    ядра.|
| <b>debug</b>             | Включает debag режим при загрузке ядра |
| <b>edd=off</b>or sdd=off | Отключает EDD(Enhanced Disk Drive). Если при загрузке Linux вы видите сообщение Probing EDD и загрузка на                                этом останавливается, тогда вам поможет параметр ядра edd=off. |
| <b>init=</b>             | Позволяет задать программу инициализации. По умолчанию используется программа /sbin/init, но вы можете                                  задать другую программу. Пример `init=/bin/sh` |
| <b>kbd-reset</b>         | Использование этой опции может помочь вам, если у вас есть проблемы с клавиатурой |
| <b>load_ramdisk=</b>     | Этот параметр сообщает ядру - нужно ли загружать образ ram-диска или нет. `0` or `1` |
| <b>maxcpus=</b>          | Число, указанное в этом параметре, ограничивает максимальное количество процессоров в режиме SMP.                                        Использование 0 эквивалентно опции nosmp. |
| <b>mem=</b>              | Определяет объем памяти, установленной в компьтере. Иногда ядро неправильно определяет объем оперативной                                памяти. Вы можете помочь ему в этом, указав параметр mem. Пример `mem=1024M` |
| <b>memtest</b>           | Программа memtest позволяет проверить оперативную память вашего компьютера |
| <b>modeset</b>           | включить KMS |
| <b>noapic</b>            | Полезен, если вы при загрузке увидите сообщение: "kernel panic — not syncing: IO-APIC + timer doesn’t                                    work!."|
| <b>noapm</b>             | Отключает APM (Advanced Power Management) — расширенное управление питанием. |
| <b>noauto</b>            | Запрещает автоматическое определение устройств. Также полезен, если при установке нужно передать параметры                              модулям ядра или непосредственно устройствам |
| <b>nodma</b>             | Отключает DMA(Direct Memory Access, прямой доступ к памяти) для всех IDE-устройств. |
| <b>nodmraid</b>          | Отключает программные RAID-массивы, организованные на уровне BIOS |
| <b>nomodeset</b>         | Если ошибка графического драйвера и система не грузится, или отключить KMS (Kernel mode setting) |
| <b>nopcmcia</b>          | Отключает PCMCIA-Карты(для ноутбуков). Полезен, если вы подозреваете, что у вас проблема с PCMCIA-картой. |
| <b>noscsi</b>            | Отключает поддержку SCSI. |
| <b>nosmp</b>             | Позволяет SMP ядру на SMP машинах работать одним процессором. Обычно используется только для отладки и                                  определения наличия зависимости конкретной проблемы от SMP. |
| <b>nousb</b>             | Отключает поддержку USB. |
| <b>pci=noacpi</b>        | Не использовать ACPI для управления PCI-прерываниями. |
| <b>quiet</b>             | «Тихий» режим, отключает большинство сообщений ядра. |
| <b>ramdisk_size=</b>     | Поскольку в действительности размер ram-диска растет динамически, по мере необходимости, должно быть                                    ограничение его размера, чтобы он не занял всю память и не оставил вас в недоумении |
| <b>ramdisk_start=</b>    | Чтобы разрешить образу ядра находиться на флоппи-диске со сжатым образом ram-диска необходимо добавить                                  команду `ramdisk_start=<смещение>` |
| <b>ro</b>                | Монтирует корневую файловую систему в режиме «только чтение». |
| <b>rw</b>                | Монтирует корневую файловую систему в режиме «чтение/запись». При использованиии этого параметра нельзя                                  запускать программы типа `fsck`. Перед запуском `fsck` нужно перемонтировать корневую файловую систему в                                режиме `ro`. |
| <b>reboot=</b>           | Позволяет задать тип перезагрузки компьютера. Возможные значения: `cold` и `warm` |
| <b>rescue</b>            | Восстановление уже установленной операционной системы |
| <b>root=устройство</b>   | Позволяет указать корневую файловую систему. Например: `root=/dev/sda5`. |
| <b>rootdelay=N</b>       | Ждать `N` секунд перед монтированием корневой файловой системы. |
| <b>rootflags=флаги</b>   | Задает флаги корневой файловой системы. |
| <b>rootfstype=тип</b>    | Задает тип корневой файловой системы. Полезен, если не удалось определить автоматически. |
| <b>rootwait</b>          | Ядро будет ждать, пока не появится устройство с корневой ФС. Полезен, когда корневая файловая система                                    расположена на съемном носителе, например на флешке. |
| <b>single</b>            | Однопользовательский режим для администрирования системы, например, в случае отказа. |
| <b>swap=</b>             | позволяет пользователю настраивать некоторые параметры виртальной памяти (VM), относящейся к своппингу на                                диск. Он может иметь следующие восемь значений: `MAX_PAGE_AGE, PAGE_ADVANCE, PAGE_DECLINE,                                              PAGE_INITIAL_AGE, AGE_CLUSTER_FRACT, AGE_CLUSTER_MIN, PAGEOUT_WEIGHT, BUFFEROUT_WEIGHT` |
| <b>text</b>              | В случае, если возникли проблемы с графической подсистемой (даже в режиме `vgal6`) можно попытаться                                      установить Linux в текстовом режиме |
| <b>toram</b>             | 	Позволяет загрузить Livecd в оперативную память (т.е. флешка(диск) потом не нужна) |
| <b>vga=режим</b>         | 	Позволяет задать VGA-режим. |
| <b>vgahi</b>             | Запуск программы установки при максимально допустимом разрешении монитора |
| <b>vgal6</b>             | Программа установки будет работать при разрешении 640x480x16 |
| <b>vgalo</b>             | Установка Linux при низком разрешении монитора. Данный параметр нужно указать, если при запуске программы                                установки с обычным разрешением монитора возникают проблемы (размытое, нечеткое изображение) |
|                  |  |





























