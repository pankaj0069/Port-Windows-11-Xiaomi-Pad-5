<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Xiaomi Pad 5 मे चलती हुई windows

## secureboot को डीसॲवल करना 
> [!Important]
> Follow this guide only if you want to disable यह गाइड सिर्फ तभी इस्तेमाल करे जब आप secureboot को डीसॲवल करना चाहते हैं और आप को पता है कि इसके क्या फायदे और नुकसान है 

### आवश्यकता 
- ```काम करता हुआ दिमाग```

- [```Android platform tools```](https://developer.android.com/studio/releases/platform-tools)

- [```Recovery Image```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/recovery.img)

- [```UEFI image (Secureboot off)```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-NoSecureboot-v3.img)

## secureboot के फायदे और नुकसान 
> डिफॉल्ट रूप से , इस गाइड मे secureboot चालू है

##### secureboot के फायदे और नुकसान 
- √ होम स्क्रीन पर कोई वाटरमार्क नहीं आएगा 
- √ जो एप्स टेस्ट मोड में नहीं चलती वो चलने लगेगी
- √ आप बड़े windows अपडेट (जेसे 22h2 से 23h2) को सीधा ही windows अपडेट से कर सकते हो
- × बस आप बिना दूसरे कंप्युटर के ड्राइवर अपडेट नहीं कर सकते

##### secureboot बंद करने के फायदे और नुकसान
- √ आप बिना दूसरे कंप्युटर के ड्राइवर अपडेट कर सकते हो बस इतना ही फायदा है 
- × होमस्क्रीन पर वॉटरमार्क दिखाई देगा 
- × कुछ एप्स और गेम जो एंटी चीट सॉफ्टवेयर के साथ आते हैं काम नहीं करेगे 
- × बड़े windows अपडेट (जेसे 22h2 से 23h2) को windows अपडेट के माध्यम से नहीं कर सकते

## secureboot बंद करना 

#### अपने rooted boot इमेज की एक बैकअप बना लो 
> आपको यह एंड्रॉयड मे जाने के लिए चाहिए होगी, अगर आप ने पहले ही बैकअप कर रखा है तो दुबारा करने की जरूरत नहीं है 

Woa helper एप मे `Backup Android boot` फंक्शन का इस्तेमाल करो या फिर मोड की हुई रिकवरी मे बूट करो य़ह cmd चलाओ 
```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

#### recovery मे बूट करना 
>  <path\to\recovery>की जगह रिकवरी इमेज की लोकेशन लगाओ
```cmd
fastboot boot <path\to\recovery.img>
```

#### mass storage mode चालू करो 
> जेसे ही आपका टेबलेट मोड की हुई recovery मे बूट हो जाए तो यह cmd चलाओ 
```cmd
adb shell msc
```

#### Windows disk manager चालू करो 
> जेसे ही टेबलेट डिस्क की तरह डिटेक्ट हो जाए तो यह cmd चलाओ 
```cmd
diskpart
```

#### टेबलेट का esp वॉल्युम चुनो 
> `list volume`का इस्तेमाल करके इसे ढूंढो इसका नाम "ESPNABU" होगा 
```diskpart
select volume <number>
```

#### Assign the letter Y
```diskpart
assign letter y
```

#### Exit diskpart
```diskpart
exit
```

#### bootloader फाइल को मोडिफाइ करो 
>  टेस्ट signing करने के लिए 
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Removing SiPolicy
> मान लो आप पहले से इंस्टॉल की हुई windows पर secureboot बंद कर रहे हो तो आपको यह फाइल डिलीट करनी पड़ेगी नहीं तो सिस्टम बूट नहीं होगा
```cmd
del Y:\EFI\Microsoft\Boot\SiPolicy.p7b
```

#### ESPNABU से ड्राइव latter हटाना 
> अगर यह काम ना करे तो अगली cmd पर चले जाए, भूतीया ड्राइव अगले रिस्टार्ट मे गायब हो जाएगी
```cmd
mountvol y: /d
```

#### fastboot मे रिबूट करो 
```cmd
adb reboot bootloader
```

#### UEFI को फ्लैश करो 
> सुनिश्चित कर ले कि आप इस पेज से No scureboot UEFI इस्तेमाल कर रहे हैं, <path\to\uefi-NoSecureboot-v3.img> की जगह UEFI की असली लोकेशन लगाये
```cmd
fastboot flash boot <path\to\uefi-NoSecureboot-v3.img>
```

> [!Important]
> सुनिश्चित कर ले कि आपने अपने एंड्रॉयड मे पुरानी UEFI की जगह नयी UEFI(बिना Scureboot वाली) डाल दी है ताकि आप भूल से गलत UEFI ना फ्लैश कर दो और फिर आपको दिक्कत हो जाए

#### Reboot to Windows मे रिबूट कर ले 
```cmd
fastboot reboot
```

## हो गया ये भी!

