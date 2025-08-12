# डेबियन गेमिंग - गाइड
[![en](https://img.shields.io/badge/lang-en-red.svg)](README.md)
[![pl](https://img.shields.io/badge/lang-pl-red.svg)](README.pl.md)
[![zh](https://img.shields.io/badge/lang-zh-red.svg)](README.zh.md)
[![es](https://img.shields.io/badge/lang-es-red.svg)](README.es.md)
[![pt](https://img.shields.io/badge/lang-pt-red.svg)](README.pt.md)
[![ru](https://img.shields.io/badge/lang-ru-red.svg)](README.ru.md)
[![de](https://img.shields.io/badge/lang-de-red.svg)](README.de.md)
[![fr](https://img.shields.io/badge/lang-fr-red.svg)](README.fr.md)
[![ja](https://img.shields.io/badge/lang-ja-red.svg)](README.ja.md)
## चरण 1 - इंस्टॉलेशन
1. डिस्क इमेज डाउनलोड करें: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.0.0-amd64-netinst.iso
2. एक बूटेबल USB ड्राइव बनाएं। आप Rufus या Etcher जैसे एप्लिकेशन का उपयोग कर सकते हैं। कुछ पुराने प्लेटफॉर्म पर, इन एप्लिकेशन से बूटेबल USB बनाने के बाद भी सिस्टम बूट नहीं हो सकता। अंतिम उपाय के रूप में, आप unetbootin (Linux) का उपयोग कर सकते हैं।
3. इंस्टॉलेशन के दौरान, इंस्टॉलर आपसे रूट पासवर्ड पूछेगा - **इस फ़ील्ड को खाली छोड़ दें!**
4. सिस्टम का मुख्य उपयोगकर्ता बनाएँ, उपयोगकर्ता नाम और पासवर्ड प्रदान करें।
5. जब आप चुनते हैं कि डेबियन को शुरुआत में कौन से पैकेज इंस्टॉल करने चाहिए, तो अपना पसंदीदा डेस्कटॉप वातावरण चुनें। मैं KDE Plasma सुझाता हूँ, लेकिन यदि आपको पता है कि आप क्या कर रहे हैं, तो आप कोई और चुन सकते हैं।

## चरण 2 - Nvidia ड्राइवर (यदि आपके पास Nvidia कार्ड नहीं है तो छोड़ दें)
टर्मिनल खोलें और निम्नलिखित कमांड चलाएँ:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get install -y nvidia-open #RTX2000 सीरीज़ या नए कार्ड के लिए
sudo apt-get install -y cuda-drivers #GTX1000 सीरीज़ या पुराने कार्ड के लिए
```

## चरण 3 - Flatpak
Flatpak Linux के लिए एक सार्वभौमिक सॉफ़्टवेयर वितरण प्रणाली है। Flatpak रिपॉजिटरी सेटअप करके, आप सिस्टम की इन-बिल्ट स्टोर से कई उपयोगी ऐप्स इंस्टॉल कर सकते हैं।
```
sudo apt install flatpak
sudo apt install plasma-discover-backend-flatpak #यदि आप KDE Plasma का उपयोग कर रहे हैं
sudo apt install gnome-software-plugin-flatpak #यदि आप Gnome का उपयोग कर रहे हैं
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## चरण 4 - Backports
Backports रिपॉजिटरी आपको डेबियन के स्थिर संस्करण पर कुछ पैकेज अपडेट करने की अनुमति देती है। महत्वपूर्ण पैकेजों में kernel, mesa, pipewire और flatpak शामिल हैं।
```
echo "deb http://deb.debian.org/debian trixie-backports main" | sudo tee /etc/apt/sources.list.d/backports.list
sudo apt update
```

Backports रिपॉजिटरी से पैकेज इंस्टॉल करने के लिए:
```
sudo apt install -t trixie-backports <पैकेज>
```

Kernel अपडेट:
```
sudo apt install -t trixie-backports linux-headers-amd64 linux-image-amd64
```

Mesa अपडेट:
```
sudo apt install -t trixie-backports libegl-mesa0
```

इसी तरह, flatpak या pipewire को अपडेट करने के लिए `<पैकेज>` को flatpak या pipewire से बदलें।

**नोट:** आज की तारीख (11.08.2025) तक backports में इन पैकेजों के नए संस्करण उपलब्ध नहीं हैं। सूची यहां देखें: https://packages.debian.org/trixie-backports/
