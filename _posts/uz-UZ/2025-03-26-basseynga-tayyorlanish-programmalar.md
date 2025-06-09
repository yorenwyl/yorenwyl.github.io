---
title: Basseyn(С piscine)ga tayyorlanish uchun zarur programmalar.
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichiga tayyorlanish uchun mo‘ljallangan, bajarilgan va izohlangan vazifalarning turli versiyalari taqdim etilgan.
author: yorenwyl
date: 2025-03-26 18:22:00 +0500
categories: [21-IT Maktab - School 21, Basseyn - C Piscine]
tags: [Basseyn - C Piscine]
pin: true
image:
  path: /school-21.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 21-IT Maktab - School 21.
media_subpath: "/assets/img/articles/2025-03-26-basseynga-tayyorlanish/"
---

---

## **Windows va MacOS Tizimlarida Samarali Ishlash uchun Qulay Vositalar**

Bugungi kunda turli xil onlayn xizmatlar va dasturlar sizning ish jarayonlaringizni sezilarli darajada soddalashtirishi mumkin. Ayniqsa, **Yandex**, **Git**, **Crow Translate**, **Git Bash** va boshqa vositalar sizga ko'p funksiyalarni taqdim etadi, masalan, **ChatGPT** ni o'rnatish, **YouTube** videolarini bir nechta tillarga tarjima qilish va boshqa turli imkoniyatlar. Quyida ular haqida batafsil ko'rsatmalar keltirilgan.

### **1. Git ni Windowsga o'rnatish va Git Bash dan foydalanish**

**Git** — bu versiyalarni boshqarish tizimi bo'lib, asosan dasturchilar tomonidan kodlarni boshqarish va bir nechta dasturchilar o'rtasida ishlashda ishlatiladi. **Windows** tizimida Git ni o'rnatish uchun quyidagi qadamlarni bajarish kerak:

#### **Git o'rnatish**

1. Git ning rasmiy saytiga kirib, Windows uchun Git installerini yuklab oling:  
   [https://git-scm.com/](https://git-scm.com/){: target="_blank"}
   
2. Installer ni ishga tushiring va o'rnatish jarayonini boshlang. O'rnatishda default sozlamalarni qabul qilishni tavsiya qilaman. Biroq, siz **Git Bash** ni o'rnatish uchun "Git Bash Here" variantini tanlashingiz mumkin.

#### **Git Bash Terminalidan Foydalanish**

**Git Bash** — bu Windowsda terminal orqali **Git** bilan ishlash imkoniyatini beradi. **Git Bash** yordamida fayllarga ko'rsatmalarni kiritish va **Git buyruqlarini** bajarish qulay bo'ladi. Git Bash terminalida Windows papkalariga ruxsat berish bilan bog'liq cheklovlar yo'q, bu esa fayllarni va papkalarni oson boshqarishga yordam beradi.

1. **Git Bash** terminalini oching.
2. Komandalarni quyidagicha kiritib, Git yordamida repozitoriya yaratish va boshqarishni boshlashingiz mumkin:

```bash
git init
git add .
git commit -m "Initial commit"
```

---

### **2. ChatGPT ni Yandex orqali o'rnatish**

**ChatGPT** ni **Yandex** orqali o'rnatish va ishlatish juda oson. **Yandex.Browser** yordamida siz saytdan to'g'ridan-to'g'ri ilova sifatida foydalanishingiz mumkin. Quyidagi qadamlar orqali bu jarayonni amalga oshirishingiz mumkin:

1. **Yandex.Browser** ni oching va **ChatGPT** rasmiy saytiga o'ting:  
   [https://chat.openai.com](https://chat.openai.com){: target="_blank"}

2. Saytga kirganingizdan so'ng, **"Добавить сайт как приложение"** tugmasini toping (bu tugma browserning yuqori o'ng burchagida bo'ladi).

3. **ChatGPT** saytini ilova sifatida qo'shish uchun ekranda ko'rsatilgan ko'rsatmalarga amal qiling. Sayt o'rnatilgach, uni **"Pusk"** menyusiga yoki **panelga** joylashtirishingiz mumkin.

Bu usul orqali siz **ChatGPT** ni alohida ilova sifatida ishga tushirishingiz va uni to'g'ridan-to'g'ri kompyuteringizda ishlatishingiz mumkin.

---

### **3. Crow Translate va OCR**

**Crow Translate** — bu tarjima qilish uchun ishlatiladigan dastur bo'lib, u **OCR (Optical Character Recognition)** texnologiyasidan foydalanadi. **OCR** yordamida siz suratdagi matnni tanib olish va tarjima qilish imkoniyatiga ega bo'lasiz.

#### **Crow Translate va OCR o'rnatish**

**Crow Translate** hozirda KDE Invent platformasida rivojlanmoqda, va u avvalgi `https://crow-translate.github.io/` manzilida mavjud emas. Yangi manziliga quyidagi havoladan o‘ting: [Crow Translate - KDE Invent](https://invent.kde.org/office/crow-translate){: target="_blank"}.

1. Agar siz **Crow Translate** ni **winget** yordamida o‘rnatmoqchi bo‘lsangiz, quyidagi amallarni bajarishingiz mumkin:

   1. **Winget yordamida Crow Translateni o‘rnatish**:
      
      Winget orqali Crow Translate’ni o‘rnatish uchun quyidagi buyruqni terminalga kiriting:

      ```Command Prompt
      winget install CrowTranslate.CrowTranslate
      ```

      Bu buyruq **Crow Translate** ni Windows tizimingizga o‘rnatadi.

   2. **O‘rnatish jarayonini tekshirish**:
      
      O‘rnatish muvaffaqiyatli bo‘lsa, Crow Translate dasturi o‘rnatilgan bo‘ladi. Uni **Start Menu** orqali topishingiz yoki terminalda `crow-translate` komandasini ishga tushirib ishga tushirishingiz mumkin.

   **Crow Translate** dasturini o'rnatish uchun [crow-translate yuklab olish](https://github.com/crow-translate/crow-translate/releases){: target="_blank"} saytiga kirib, Windows uchun .exe faylni yuklab olishingiz ham mumkin.
   
2. Dastur ochilganidan so'ng, **OCR** funksiyasini faollashtiring. **OCR** funksiyasi uchun data file [tilini yuklab olish](https://github.com/tesseract-ocr/tessdata){: target="_blank"}.

![Crow Translate sozlamalari](crow-translate.png){: width="972" height="589" }
_Crow Translate sozlamalari_

3. OCR orqali chiqarilgan matnni tarjima qilish uchun kerakli tilni tanlang va tarjima jarayonini boshlang.

---

### **4. YouTube Videolarini Tarjima qilish va ovozli Tarjima**

**Yandex** ning yangi versiyasida **YouTube** videolarini tarjima qilish funksiyasi mavjud. Bu sizga videolarni o'zingiz bilmagan tillarda tomosha qilishda yordam beradi.

![Yandex logo](yandex.jpg){: width="972" height="589" }
_OvozliTarjima Funksiyasi_


#### **YouTube-da Tarjima qilish**

1. **YouTube** videosini oching.
2. Video oynasining **so'zli ikonkasini** bosib, kerakli tilni tanlang. **Yandex brauzerining** **tarjima qilish** funksiyasi orqali videolarni 8 ta tilga o'zgartirish mumkin.
3. Siz tanlagan tilga video subtitrlarini avtomatik tarzda tarjima qilishingiz mumkin.

---

### **5. Punto Switcher va Klaviatura Tilini Avtomatik O'zgartirish**

**Punto Switcher** — bu klaviatura tilini avtomatik tarzda almashtiradigan dastur. **Windows** tizimida bu dastur yordamida tezda tilni almashtirish mumkin. **Punto Switcher** ni o'rnatish va ishlatish jarayonini ko'rib chiqamiz:

1. **Punto Switcher** ni rasmiy saytidan yuklab oling:  
   [https://puntoSwitcher.ru/](https://puntoSwitcher.ru/){: target="_blank"}
   
2. O'rnatish jarayonida ko'rsatmalarga amal qiling.

3. O'rnatilganidan so'ng, **Punto Switcher** avtomatik tarzda klaviatura tilini aniqlaydi va tezda ruscha yoki inglizcha tilga o'tishni amalga oshiradi.

---

### **Xulosa**

Ushbu maqolada, sizga **Yandex** ning yangi imkoniyatlari, **ChatGPT** ni Yandex orqali o'rnatish, **Git** yordamida versiyalarni boshqarish, **Crow Translate** va **OCR** funksiyasidan foydalanish, shuningdek, **YouTube** videolarini tarjima qilish, **Punto Switcher** dasturidan foydalanish haqida ko'rsatmalar berildi. **Yandex** ning yangi versiyasida nafaqat tilni avtomatik o'zgartirish, balki **ovozli tarjima** kabi qiziqarli funksiyalar ham mavjud bo'lib, ular sizning ish jarayoningizni sezilarli darajada samarali qiladi.

- [`Tugallangan С piscine` maqolasiga o'tish](../tugallangan-c-piscine/){: target="_blank"}