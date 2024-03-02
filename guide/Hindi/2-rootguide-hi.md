<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Running Windows on the Xiaomi Pad 5

## रूट करने की प्रक्रिया 
> [!NOTE]
> **अगर आपने पहले से ही रूट कर रखा है तो इस पेज पर दिए गए स्टेप छोड़ दे और अगले पेज पर चले जाए **

### सबसे जरूरी चीज 
- ```दिमाग भाई दिमाग ```
  
- [```Android boot backup```](/guide/English/1-partition-en.md#Make-a-backup-of-your-existing-boot-image) (जो आपने पहले पेज पर बैकअप लिया था )


## Patch boot 

- ```normal_boot.img``` को कंप्युटर के ```platform tools``` फ़ोल्डर से टेबलेट मे कॉपी कर ले। 

- [Magisk app](https://github.com/topjohnwu/Magisk/releases/latest) को डाउनलोड करके टेबलेट में इंस्टाल कर ले।
  
- magisk ऐप खोले ```Install``` बटन पर क्लिक करें। फिर ```Select and Patch a File``` पर क्लिक करें और ```normal_boot.img``` जो कि आपने कंप्युटर से टेबलेट मे डाली थी को सेलेक्ट करे। अब ```Let's Go``` बटन पर क्लिक कर दे ओर प्रोसेस पूरा होने दें।
  
- अब ```magisk_patched....img``` बूट इमेज को टेबलेट के ```Downloads``` फ़ोल्डर से उठा कर कंप्युटर के ```platform tools``` फ़ोल्डर मे कॉपी कर दे। 

- अब fastboot mode मे reboot करे 
  
- platform tools फ़ोल्डर में command prompt को खोले 

 ## अब magisk से पैच की हुई बूट इमेज को टेबलेट मे flash करना 
 >  `<magisk_patched.img>` की जगह असली ```magisk_patched.img```का path डाले 
```cmd
fastboot flash boot <magisk_patched.img>
```

### [अगला चरण : Windows इंस्टॉल करना ](/guide/hindi/3-install-hi.md)
