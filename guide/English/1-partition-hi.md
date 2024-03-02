<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Running Windows on the Xiaomi Pad 5

## इंस्टॉल करना 



### आवश्यक शर्तें 
-  ```खोपड़ी मे दिमाग```
  
- [```रिकवरी इमेज ```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/recovery.img)

- [```एंड्रॉयड प्लेटफॉर्म टूल्स ```](https://developer.android.com/studio/releases/platform-tools)

### टिप्पणियां :
> [!टिपणी]
> नहीं पता केसे स्टार्ट करे ? पहले डाउनलोड फाइल अनजीप करो [```Android platform tools```](https://developer.android.com/studio/releases/platform-tools), जेसे की ```"C:\platform-tools"``` उसके बाद  ```command prompt``` या फिर `powershell`को as administrator and type:
```cmd
cd "path\to\platform-tools"
```
> Replace  `"path\to\platform-tools"` with the actual path of the platform tools folder


> [!Warning]\
> if you delete any partitions via diskpart later on or now, windows will send a ufs command that gets misinterpreted which erase all your ufs
> 
> All your data will be erased! Backup now if needed.
> 
> These commands have been tested.
> 
> DO NOT REBOOT YOUR TABLET if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/nabuwoa)
>
> **PLEASE DON'T USE OUTDATED VIDEO GUIDES ON YOUTUBE OR ANY OTHER PLATFORM! THESE VIDEOS ARE OUTDATED AND YOU CAN BRICK YOUR DEVICE USING THEM! IF YOU NEED A VIDEO GUIDE, USE THIS [NEW VIDEO GUIDE](https://youtu.be/BbgTbTGbXYg) FROM [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA)**


### Partitioning your device and backup boot

#### Boot recovery through the PC with the command
```cmd
fastboot boot <recovery.img>
```
#### Partitioning your device

> If it asks you to run it once again, do so

> This is **optional**, but you can also **set custom sizes (by default, it splits the storage in half)**

> To set custom sizes do ```adb shell partition [TARGET WINDOWS SIZE IN GB]```

> Make sure you do not add GB at the end, just the number

```cmd
adb shell partition
```

### Make a backup of your existing boot image
```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/normal_boot.img" && adb pull /tmp/normal_boot.img
```


#### Check if Android still starts
> Reboot to check if Android still works. If it doesn't boot, wipe all data in recovery and try again.

```cmd
adb reboot
```


### [Next step: Get Root](/guide/English/2-rootguide-en.md)
