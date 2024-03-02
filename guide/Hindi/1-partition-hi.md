<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Running Windows on the Xiaomi Pad 5

## इंस्टॉल करना 



### आवश्यक शर्तें 
-  ```खोपड़ी मे दिमाग```
  
- [```रिकवरी इमेज ```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/recovery.img)

- [```एंड्रॉयड प्लेटफॉर्म टूल्स ```](https://developer.android.com/studio/releases/platform-tools)

### टिप्पणियां :
> [!NOTE]
> 
> नहीं पता केसे स्टार्ट करे ? पहले डाउनलोड फाइल अनजीप करो [```Android platform tools```](https://developer.android.com/studio/releases/platform-tools), जेसे की ```"C:\platform-tools"``` उसके बाद  ```command prompt``` या फिर `powershell`को as administrator शुरू करे और टाइप करे :
```cmd
cd "path\to\platform-tools"
```
> `"path\to\platform-tools"` इस पाथ की जगह जो अभी पाथ है प्लेटफॉर्म टूल फ़ोल्डर का वो डाले


> [!Warning]\
> अगर आप diskpart द्वारा कोई partation अब या बाद में डिलीट करते है तो, windows एक ufs कमांड भेजेगी और उसका सिस्टम गलत मतलब निकाल लेगा और आपकी सारी स्टोरेज क्लीन हो जाएगी मतलब सारे partation जो टेबलेट के लिए जरूरी है और डिवाइस ब्रिक हो जाएगी। 
> 
> आपका सारा डाटा डिलीट हो जाएगा तो पहले ही बैकअप ले लेंवे अगर आप के लिए आपका डाटा जरूरी है।
> 
> ये सारी कमांड टेस्ट की हुई है।
> 
> अपने टेबलेट को बीच में रीबूट ना करे अगर आपको लगता है कि आपसे कोई गलती हो गयी है, तो तुरन्त मदद के लिए [Telegram chat](https://t.me/nabuwoa) पर जाए 
>
> **कृपया पुरानी वीडियो गाइड जो कि यूट्यूब और अन्य प्लेटफॉर्म पर मौजूद है उनका उपयोग ना करे ये आपकी टेबलेट को ब्रिक कर सकती है। अगर फिर भी वीडियो गाइड चाहिए तो ये सिर्फ ये नई गाइड यूज करे 
> [NEW VIDEO GUIDE](https://youtu.be/BbgTbTGbXYg) FROM [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA)**


### windows के लिए Partition बनाना और बूट इमेज का बैकअप लेना

#### कंप्युटर के द्वारा ये कमांड लगाकर कस्टम रिकवरी को बूट करे
```cmd
fastboot boot <recovery.img>
```
#### अब हमको Partition बनाने है 

>अगर ये कमांड को दुबारा चलाने को बोले तो चला दे

> यह आप पर है यदि आप windows के लिए कस्टम स्टोरेज स्पेस चाहते हैं **(वेसे ये कुछ ना करने पर एंड्रॉयड और windows दोनों को ½ ½ स्टोरेज देगी)**

> कस्टम स्टोरेज साइज सेट करने के लिए ```adb shell partition [जितना स्टोरेज स्पेस चाहिए वो यहां लिखो]```

>ध्यान रखे लास्ट मे GB ना लगाएं सिर्फ नम्बर लगाएं। 

```cmd
adb shell partition
```

### अब एंड्रॉयड वाली बूट इमेज का बैकअप लेने के लिए ये कमांड चलाए। 
```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/normal_boot.img" && adb pull /tmp/normal_boot.img
```


#### अब चेक करे कि एंड्रॉयड बूट हो रहा है या नहीं 
> एंड्रॉयड अब भी चल रहा है इसको जाँचने के लिए टेबलेट को reboot करे। अगर ना चले तो रिकवरी मे जाके wipe all data करे और फिर से कोशिश करे 
>

```cmd
adb reboot
```


### [अगला चरण : रूट करना ](/guide/hindi/2-rootguide-hi.md)
