<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Xiaomi Pad 5 पर windows इस्तेमाल करना
> [!WARNING]
> **कृपया किसी भी वीडियो गाइड का उपयोग ना करे वे लगभग सभी पुरानी गाइड है और टेबलेट को ब्रिक कर सकती है। अगर फिर भी वीडियो गाइड यूज करनी है तो सिर्फ यह यूज करे [VIDEO GUIDE](https://youtu.be/BbgTbTGbXYg) BY [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA)**

## इंस्टॉल कराना 
> [!NOTE]
> अब CMD या powershell को एडमिनिस्ट्रेटर की तरह खोलना पड़ेगा, फिर platform-tools फ़ोल्डर को `cd C:\path\to\platform-tools` command का इस्तेमाल करते हुए एक्सेस करे, path को platform-tools फ़ोल्डर के वास्तविक पाथ से बदल दे।
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

  
  

### अब हम windows करेगे इंस्टाल

> Replace `<path\to\install.esd>`की जगह install.esd (इसका नाम 'install.wim' भी हो सकता है)की जो अभी जगह है उसकी लोकेशन डाल दो

```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> अगर आप को `Error 87`मिलता है , check the index of your image with तो इस `dism /get-imageinfo /ImageFile:<path\to\install.esd>`cmd के द्वारा अपनी इमेज फाइल का इंडेक्स ज्ञात करो, फिर `index:6` की जगह जो नया इंडेक्स नंबर आप को पता चला है वो लगा दो। 


### अब करना है Drivers को इंस्टॉल 

> आप drivers को [यहां](https://github.com/map220v/MiPad5-Drivers/releases/latest) से डाउनलोड कर सकते हो। 

>अब Drivers वाला फ़ोल्डर खोलो और OfflineUpdater.cmd को चला दो 
>
>अगर यह बोले `"Automatic WINNABU detection failed! Enter Drive Letter manually"` तो **`X`** डाल दो 


### Windows के लिए EFI के लिए bootloader फाइल को बनाना 
>अगर बूट फाइल को कॉपी करते समय कोई त्रुटि आती है,तो check `diskpart` मे जाके चेक करो की ESPNABU के पास अभी भी Y अक्षर है अगर नहीं है कि कोई और अक्षर(जेसे की P) डाल दो और नीचे वाले cmd मे Y की जगह जो अभी आप ने नया अक्षर डाला है वो डाल दो। 
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

## Remove the drive letter for ESPNABU का ड्राइव अक्षर हटाना
> If this does not work अगर य़ह काम ना करे,तो इसको छोड़ कर आगे बढ़ जाए भूतीया अगली बार रिबूट करने पर अपने आप गायब हो जाएगी। 
>
```cmd
mountvol y: /d
```


## Windows में बूट करना 

### इस cmd द्वारा रूट की हुई boot image का एक बैकअप बना लो 

```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

### bootloader मे रिबूट करो

```cmd
adb reboot bootloader
```

### UEFI image को डाउनलोड करके फ्लैश करो 
>  [UEFI image](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img) डाउनलोड करो 

```cmd
fastboot flash boot <path to image>
```

## इस cmd से Windows मे रिबूट करो 
```cmd
fastboot reboot
```

> [!NOTE]
> पहले बूट पर, यह कोई wifi नेटवर्क नहीं दिखाएगा तो पावर बटन को कई देर तक दबा कर टेबलेट को रिबूट कर ले और आपको नेटवर्क दिखाई देने लग जायेगे। अगर अभी आपको एक popup दिखाई देता है जिसमें लिखा हुआ है "could not connect" तो लगभग 5 बार retry करे जब तक य़ह काम करने लगे 

### एंड्रॉयड मे वापिस बूट करना 
After Windows has been set up जेसे ही windows का सेटअप पूरा हो जाए,तो resart बटन को दबाये ना कि shutdown को जेसे ही ये रिस्टार्ट हो जाए पावर बटन और वॉल्युम कम करने के बटन को एक साथ दबा कर टेबलेट को fastboot मोड मे ले जाए। 
> अब बैकअप की हुई बूट इमेज को फ्लैश करे जिससे आप फिर से एंड्रॉयड को एक्सेस कर पाए। 

```cmd
fastboot flash boot rooted_boot.img
```

```cmd
fastboot reboot
```

### [आखिरी चरण : डुअल बूट को सेटअप करना](Hindi/dualboot-en.md)
