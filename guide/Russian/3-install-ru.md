<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Windows на Xiaomi Pad 5
> [!WARNING]
> **ПОЖАЛУЙСТА, НЕ ИСПОЛЬЗУЙТЕ УСТАРЕВШИЕ ВИДЕОГИДЫ НА YOUTUBE ИЛИ ЛЮБОЙ ДРУГОЙ ПЛАТФОРМЕ! ЭТИ ВИДЕО УСТАРЕЛИ, И ВЫ МОЖЕТЕ ЗАБЛОКИРОВАТЬ СВОЕ УСТРОЙСТВО, ИСПОЛЬЗУЯ ИХ! ЕСЛИ ВАМ НУЖЕН ВИДЕОГИД, ВОСПОЛЬЗУЙТЕСЬ ЭТИМ [НОВЫЙ ВИДЕОГИД](https://youtu.be/BbgTbTGbXYg) ОТ [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA)**


## Установка

### Требования

- [```Образ UEFI```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img)
  
- [```Драйверы```](https://github.com/map220v/MiPad5-Drivers/releases/latest)

- [```ARM Windows esd```](https://worproject.com/esd) (Выберите - Version:  ```11``` Build:  ```22631.2861``` Architecture:  ```ARM64``` Edition:  ```CLIENT``` Language:  ```Выберите ваш язык```)
  
### Перезапустите рекавери чтобы начать установку Windows

```cmd
fastboot boot <recovery.img>
```

#### Запустите msc
> Если скрипт попросит запустить его ещё раз, то так и сделайте

```cmd
adb shell msc
```

### Привязка букв к разделам
  

#### Запустите Менеджер дисков Windows

> Как только планшет определился как диск

```cmd
diskpart
```


#### Привязка буквы  `X` к разделу Windows

#### Выберите Windows раздел планшета
> Используйте команду `list volume` чтобы найти разделы "WINNABU" и "ESPNABU"

```diskpart
select volume <number>
```

#### Привяжите букву X
```diskpart
assign letter x
```

### Привязка буквы  `Y`  к разделу ESP

#### Выберите ESP раздел планшета
> Используйте команду `list volume` чтобы найти его, обычно это последний раздел

```diskpart
select volume <number>
```

#### Привяжите букву Y

```diskpart
assign letter y
```

#### Закройте diskpart
```diskpart
exit
```

  
  

### Установка Windows
> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> если вы получили `Ошибка 87`, проверьте индекс вашего образа используя `dism /get-imageinfo /ImageFile:<путь\к\install.esd>`, затем замените `index:6` существующим номером индекса Windows 11 Pro в вашем образе 


### Установка драйверов

> Вы можете скачать драйвера [тут](https://github.com/map220v/MiPad5-Drivers/releases/latest)

> Если он напишет `"Automatic WINNABU detection failed! Enter Drive Letter manually"`, введите **`X`**

```cmd
 Откройте папку с драйверами и заустите OfflineUpdater.cmd
```

### Создайте файлы загрузчика Windows для EFI
> Если при копировании загрузочных файлов возникает ошибка, откройте `diskpart', чтобы проверить, есть ли у ESPNABU буква Y. Если это не так, добавьте любую другую букву (например, K) и замените Y в приведенной ниже команде на указанную букву соответственно
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```
## Удалите букву диска для ESPNABU, чтобы избежать появления фантомной буквы диска

```cmd
mountvol y: /d
```

## Запуск Windows

### Создайте резервную копию текущего boot-образа Android

> [!NOTE]
> **Теперь вернитесь в командную строку platform tools**
```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

### Перезапустите планшет в fastboot

```cmd
adb reboot bootloader
```

### Скачайте и прошейте образ UEFI 
> Скачайте [образ UEFI](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img)
```cmd
fastboot flash boot <путь к образу UEFI>
```
## Перезагрузитесь в Windows
```cmd
fastboot reboot
```
> [!NOTE]
> При первой загрузке Windows он не увидит никаких сетей Wi-Fi, просто перезагрузите его, удерживая нажатой кнопку питания, а после перезагрузки, когда вы попытаетесь подключиться к своей сети и увидите "мороженое", нажмите "повторить попытку" 7 раз

### Загрузка в Android
После настройки Windows нажмите кнопку перезапуска в Windows (НЕ ЗАВЕРШЕНИЕ РАБОТЫ), затем, когда она перезапустится, удерживайте "уменьшение громкости" + "питание", чтобы перезагрузиться обратно в fastboot
> Прошейте скопированный boot-образ в fastboot

```cmd
fastboot flash boot rooted_boot.img
```

```cmd
fastboot reboot
```
## Готово!
[![```Telegram```](https://img.shields.io/badge/Chat-Telegram-brightgreen.svg?logo=telegram&style=flat-square)](https://t.me/nabuwoa)
### ```Вы можете присоедениться к нашему чату Telegram что-бы получать последние новости проекта```
### [Последний шаг: Настройка двойной загрузки](dualboot-ru.md)
