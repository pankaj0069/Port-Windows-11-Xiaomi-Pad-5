<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Xiaomi Pad 5 पर windows इस्तेमाल करना
> [!WARNING]
> **कृपया किसी भी वीडियो गाइड का उपयोग ना करे वे लगभग सभी पुरानी गाइड है और टेबलेट को ब्रिक कर सकती है। अगर फिर भी वीडियो गाइड यूज करनी है तो सिर्फ यह यूज करे [VIDEO GUIDE](https://youtu.be/BbgTbTGbXYg) BY [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA)**

## इंस्टॉल कराना 
> [!NOTE]
> अब CMD या powershell को एडमिनिस्ट्रेटर की तरह खोलना पड़ेगा, फिर platform-tools फ़ोल्डर को `cd C:\path\to\platform-tools` command का इस्तेमाल करते हुए एक्सेस करे, path को platform-tools के वास्तविक पाथ से बदल दे।
>सारी गाइड मे एक ही cmd या powershell विंडों यूज करे इसे बंद ना करे।

### आवश्यक फाइल 
- ```बुद्धी ```

- [```UEFI image```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img)
  
- [```ARM Windows esd```](https://worproject.com/esd) (Select - Version:  ```11``` Build:  ```22631.2861``` Architecture:  ```ARM64``` Edition:  ```CLIENT``` Language:  ```select your language```)
    
- [```Drivers```](https://github.com/map220v/MiPad5-Drivers/releases/latest)

### windows इन्स्टाल करने के लिए फिर से रिकवरी मे बूट करे

```cmd
fastboot boot <recovery.img>
```

####  msc एग्जीक्यूट करे 

> अगर यह आप को फिर से cmd रन करने को बोले तो कर दे

```cmd
adb shell msc
```
### डिस्क पर latter Assign करना 
  

#### Windows disk manager को शुरू करे 

> एक बार Xiaomi Pad 5 डिस्क की तरह दिखाई देने लगे तो आगे बडे 

```cmd
diskpart
```


#### windows वॉल्युम पर `X` Assign करना

#### टेबलेट पर Windows volume को चुनें 
> `list volume` cmd का इस्तेमाल करके इसको ढूँढे इसका नाम "WINNABU" होगा। 

```diskpart
select volume <number>
```

#### इसपर अक्षर X को assign करे 
```diskpart
assign letter x
```

### ESP वॉल्युम पर `Y` assign करना

#### टेबलेट का esp volume को चुनें
> `list volume`cmd का इस्तेमाल करके इसको ढूँढे इसका नाम "ESPNABU" होगा। 

```diskpart
select volume <number>
```

#### Assign the letter इसपर अक्षर Y को assign करे 

```diskpart
assign letter y
```

#### diskpart से निकल जाएं 
```diskpart
exit
```

  
  

### Install

> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, then replace `index:6` with the actual index number of Windows 11 Pro in your image


### Install Drivers

> You can download the Drivers [here](https://github.com/map220v/MiPad5-Drivers/releases/latest)

> If it says `"Automatic WINNABU detection failed! Enter Drive Letter manually"` type **`X`**

```cmd
 Open the folder with Drivers and run OfflineUpdater.cmd
```

### Create Windows bootloader files for the EFI
> If an error occurs when copying boot files, check `diskpart` to see if ESPNABU still has letter Y. If it does not, add any other letter (such as K) and replace the Y in the below command with said letter respectively
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

## Remove the drive letter for ESPNABU
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```


## Boot into Windows

### Make a backup of your rooted boot image

```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

### Reboot to bootloader 

```cmd
adb reboot bootloader
```

### Download and flash the UEFI image
> Download the [UEFI image](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img)

```cmd
fastboot flash boot <path to image>
```

## Reboot to Windows
```cmd
fastboot reboot
```

> [!NOTE]
> On the first Windows boot, it will not see any Wi-Fi networks. Restart your tablet by holding down the power button until it restarts. After the reboot, it will be fixed. If you get a pop-up saying "Could not connect", press retry until it works (usually 5 times)

### Boot back into Android
After Windows has been set up, press the restart button in Windows (NOT SHUTDOWN), then as it restarts, hold `volume down` + `power`to reboot back to fastboot
> Use your backup boot image and flash it in fastboot to return to Android

```cmd
fastboot flash boot rooted_boot.img
```

```cmd
fastboot reboot
```

### [Last step: Set up Dualboot](dualboot-en.md)
