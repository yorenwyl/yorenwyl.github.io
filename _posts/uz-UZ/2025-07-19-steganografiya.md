---
title: "🕵️‍♂️ Steganografiya: maxfiy axborotni yashirish san’ati"
description: Ushbu maqolada IT dunyosiga ta'luqli xabar va yangilikar taqdim etilgan.
author: yorenwyl
date: 2025-07-19 19:56:29 +0500
categories: [Yangiliklar]
tags: [Cybersecurity]
pin: true
image:
  path: /mona_lisa.jpg
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: "Mona Lisa suratidagi steganografiya qo'llanilgan misol"
media_subpath: "/assets/img/articles/2025-07-10-xabarlar/"
---

## Ta’rifi

Steganografiya — axborotni yashirin uzatish usuli bo‘lib, xabar mavjudligini yashirishga xizmat qiladi. Shifrlashdan farqli o‘laroq, xabar oddiy matn, rasm, audio yoki video ichida ko‘rinmas shaklda joylashtiriladi.

## Tarixi

- **Qadimgi Yunoniston (miloddan avvalgi V asr)**: Gerodot xabarlarning bosh terisiga tatuirovka qilinib, soch o‘sgach yuborilganini yoki yog‘och taxtaga yozilib, mum bilan qoplanganini tasvirlagan.
- **Qadimgi Xitoy**: Tuxum qobig‘iga yozilgan xabarlar mum bilan yopilgan.
- **O‘rta asrlar**: Limon sharbati yoki sutdan tayyorlangan siyohlar isitilganda ko‘rinadigan matnlar sifatida ishlatilgan. Islom olamida al-Kindiy matnlarda yashirin kodlar qo‘llagan.
- **Uyg‘onish davri**: Johannes Trithemiusning “Steganographia” asari (1518) yashirin xabarlarni kodlash usullarini taqdim etgan.
- **XX asr**: Mikrofilm, fotosuratlar va she’rlar orqali maxfiy xabarlar uzatilgan. Ikkinchi jahon urushida Navajo kod yozuvchilari steganografik usullardan foydalangan.

## Zamonaviy Steganografiya

Raqamli steganografiya quyidagi formatlarda qo‘llaniladi:

- **Rasm**: JPEG, PNG fayllarida Least Significant Bit (LSB) usuli orqali.
- **Audio/Video**: MP3, WAV, MP4 fayllarida shovqin yoki frekvensiyalarga yashirish.
- **Matn**: Unicode zero-width belgilar (masalan, zero-width space, zero-width joiner) orqali.
- **HTML/CSS**: Kod ichida bo‘sh joylar yoki maxsus belgilar bilan.

## StegCloak Vositasida Telegram Orqali Yashirin Xabar

StegCloak — JavaScript asosidagi vosita bo‘lib, zero-width Unicode belgilar orqali maxfiy xabarni oddiy matn ichiga yashiradi. Onlayn platforma: [stegcloak.surge.sh](https://stegcloak.surge.sh).

### Yashirish Jarayoni

![Yashirish](stg1.png){: width="972" height="589" }
_Yashirish jarayoniga misol_

- Saytga kirib, “MESSAGE” maydoniga oddiy matn yoziladi (masalan, “Salom, yaxshimisiz?”).
- “Secret” maydoniga maxfiy xabar kiritiladi (masalan, “Uchrashuv 22:30da”).
- Ixtiyoriy parol qo‘yiladi (masalan, “123456”).
- “Hide” tugmasi bosiladi, natija Telegram orqali yuboriladi.

### Ochish Jarayoni

![Ochish](stg.png){: width="972" height="589" }
_Ochish jarayoniga misol_

- Telegramdan olingan matn “Cover text” maydoniga joylanadi.
- Parol kiritiladi (agar ishlatilgan bo‘lsa).
- “Reveal” tugmasi orqali yashirin xabar ko‘rinadi.

Zero-width belgilar tufayli xabar ko‘zga ko‘rinmaydi va faqat StegCloak orqali ochiladi.

## Siyosiy Steganografiya

### Arnold Schwarzenegger: YouTube Murojaati (2023)

2023-yil may oyida Arnold Schwarzenegger YouTube videosida Rossiyadagi senzura va urush targ‘ibotiga qarshi murojaat qildi. Subtitrlarda zero-width Unicode belgilar orqali yashirin siyosiy xabar joylashtirildi, u oddiy tomoshabinlar uchun ko‘rinmas edi, lekin tahlil vositalari orqali aniqlandi.

### Schwarzeneggerning Veto Maktubi (2009)

2009-yil 27-oktabrda Kaliforniya gubernatori sifatida Schwarzenegger Assembly Bill 1176 qonun loyihasini rad etdi. Veto maktubining satrlari bosh harflari “FUCK YOU” iborasini hosil qiladi:

> To the Members of the California State Assembly:  
> 
> **I** am returning Assembly Bill 1176 without my signature.  
> 
> **F**or some time now I have lamented the fact that major issues are overlooked while many  
> **u**nnecessary bills come to me for consideration. Water reform, prison reform, and health  
> **c**are are major issues my Administration has brought to the table, but the Legislature just   
> **k**icks the can down the alley.  
> 
> **Y**et another legislative year has come and gone without the major reforms Californians  
> **o**verwhelmingly deserve. In light of this, and after careful consideration, I believe it is  
> **u**nnecessary to sign this measure at this time.  
> 
> Sincerely,
> 
> Arnold Schwarzenegger

**Bosh harflar**: I, F, Y → “FUCK YOU” iborasining bir qismi sifatida talqin qilingan. Statistika professori Philip Stark tasodif ehtimoli past ekanini ta’kidlagan ([stat.berkeley.edu](https://stat.berkeley.edu)).

## Xulosa

Steganografiya qadimiy usullardan zamonaviy raqamli texnologiyalargacha rivojlanib, senzura ostida axborot uzatish, maxfiy muloqot va siyosiy norozilik vositasi sifatida qo‘llanilmoqda. Schwarzeneggerning misollari va StegCloak kabi vositalar uning amaliy ahamiyatini ko‘rsatadi.

## Manbalar

- [web.williams.edu](https://web.williams.edu) — Asl veto maktubi
- [stat.berkeley.edu](https://stat.berkeley.edu) — Statistika tahlili
- [theatlantic.com](https://theatlantic.com), [californiaglobe.com](https://californiaglobe.com) — Ommaviy axborot vositalari
