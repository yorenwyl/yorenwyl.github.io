---
title: SS7 Qo‘rquv va xavf orqasidagi haqiqat
description: axborot xavfsizligi, tarmoq texnologiyalari, uyali aloqa.
author: yorenwyl
date: 2025-06-27 01:53:00 +0500
categories: [Yangiliklar, Kiberxavfsizlik]
tags: [Cybersecurity]
pin: true
math: true
mermaid: true
image:
  path: /blackhole.gif
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Qora tuynukni dumini qara 1-yanvardan keyin eshik yopiladi.
media_subpath: '/assets/img/articles/2025-03-26-basseynga-tayyorlanish/'
---

Ignorance is bliss – “Bilmaslik – baxtdir”
>  Muallifi: ingliz shoiri Thomas Gray, 1742-yildagi "Ode on a Distant Prospect of Eton College" asaridan:
>  "Where ignorance is bliss, ’tis folly to be wise."

> `Hamma` biladigan va hech qanday qiymatga ega emas deyiladigan maqola! Aqllilar olg'a bu saytdan chiqib ketinglar! 
{: .prompt-tip }

SS7 (Signaling System 7 qisqartmasi) — bu "kallasi ishlaydigan" botaniklar tomonidan hamma uchun o'ylab topilgan xu***a. 

!21 dan tashqarida so'kish mumkin.

SS7 (Signaling System 7 qisqartmasi) — bu telekommunikatsiya kompaniyalari o‘zaro muloqot qilish uchun ishlatadigan protokoldir.

Bu yirik kompaniyalar o‘rtasidagi tarmoqaro protokol sifatida, u juda katta darajadagi ishonchni o‘z ichiga oladi. Ya’ni, agar sizga SS7 orqali server bilan gaplashishga ruxsat berilgan bo‘lsa, deyarli istalgan narsani aytishga ham ruxsat berilgan bo‘ladi.

Odamlar “SS7 hujumlari” haqida gapirganda, odatda boshqa bir telekom kompaniyasiga telefon raqamini o‘z tomoniga yo‘naltirishni buyurishni nazarda tutishadi. Bu orqali SMS orqali ikki faktorli autentifikatsiyani (MFA) chetlab o‘tish mumkin — agar men Google’ning telefon provayderiga sizning raqamingiz menga tegishli deb ayta olsam, Google hisobingizga kirishga harakat qilganimda tasdiqlovchi kod menga yuboriladi, sizga emas.

Bu SS7 doirasida hatto yuqori darajadagi yoki shubhali harakat ham hisoblanmaydi. Axir har safar sizning telefoningiz boshqa kompaniya minorasiga ulanayotganida, u boshqa operatorlarga: “Hey, bu raqam endi mendan,” deb xabar berishi kerak. Bu oddiy, kundalik hol.

Dunyo bo‘ylab bir nechta yomon obro‘ga ega xalqaro telekom kompaniyalari mavjudki, ularga xakerlar kirib olgan yoki hatto ulardan SS7 tarmog‘iga kirish huquqini pul evaziga sotib olishgan — bu orqali ular ommaviy tarzda SMS MFA kodlarini o‘g‘irlashgan. Himoyalanuvchi sifatida siz bunday hujumlarga qarshi ko‘p narsa qila olmaysiz, faqatgina SMS o‘rniga ilova orqali ishlaydigan autentifikatsiya yoki U2F (aparatli xavfsizlik kalitlari) kabi xavfsizroq usullarga o‘tishingiz mumkin.

Izoh (Sharp_Cable124):
Yaxshi javob. Agar kimdir bu haqiqatdan yiroq deb o‘ylayotgan bo‘lsa, men o‘z ko‘zim bilan internetda kimdir tarmoqqa SS7 tunneli orqali kirish huquqini oyiga bir necha ming yevroga sotayotganini ko‘rganman. Menimcha, ko‘pchilik bu protokolning murakkabligi va kam tanilganligi sababli xavfsiz deb o‘ylaydi. Shuningdek, mening sharhim bunga post yozilishiga sabab bo‘lganidan faxrlanaman — bu mavzu hanuzgacha juda muhim. SMS orqali 2FA (ikki faktorli autentifikatsiya) xavfsiz EMAS.

### **SS7: Qo‘rquv va xavf orqasidagi haqiqat**

Yaqinda mobil telefonlarni kuzatish va himoyalash usullari haqida maqola e’lon qilgan edim. O'chirildi! Skriptni olmaganlar battar bo'linglar! Sizga bu ham kam. Endi esa bir aniq tahdid — SS7 protokoli orqali amalga oshiriladigan hujumlar haqida gaplashamiz. SS7 haqiqatan ham shunchalik xavflimi?

---

### **SS7 tarixi**

SS7 (Signaling System №7) — telefon tarmoqlarida xizmat ko‘rsatuvchi signal almashuvini ta’minlovchi protokol. Bu tizim 1970-yillarda ishlab chiqilgan va dastlab shunchaki ulanish, raqam uzatish, liniya bandligi kabi oddiy funksiyalar uchun mo‘ljallangan edi. Ammo telefon tarmoqlari murakkablashgan sayin, SS7 butun dunyo bo‘ylab yagona aloqa standartiga aylandi.

SS7 o‘z vaqtida katta ijobiy o‘zgarishlar olib keldi — yangi xizmatlar (SMS, AON, qayta yo‘naltirish) aynan uning tufayli paydo bo‘ldi. Biroq muammo shunda ediki, bu protokol *umuman shifrlanmagan edi*. Ya’ni, signal kanali tashqi foydalanuvchilardan yashirin bo‘lgani sababli, ishlab chiquvchilar ma’lumotlarni shifrlashga hojat yo‘q deb hisoblashgan.

---

### **Qanday qilib SS7 zaiflikka aylandi?**

2000-yillarda SS7 funksiyalarini IP tarmoqlari orqali bajaradigan yangi SIGTRAN protokoli paydo bo‘ldi. Bu bilan internet orqali SS7 kanaliga kirish mumkin bo‘lib qoldi. Shifrlash yo‘qligi va paket yuboruvchisi tekshirilmasligi sababli, hujumchi oddiy kompyuter va maxsus dastur orqali istalgan telefonni kuzatishi, suhbatlarni tinglashi yoki SMSlarni o‘qishi mumkin bo‘lib qoldi.

Bu hujumlarni amalga oshirish uchun jismoniy yaqinlik shart emas — dunyoning istalgan nuqtasidan amalga oshirish mumkin.

---

### **Nimalar qilsa bo‘ladi?**

SS7 orqali hujum qilgan shaxs quyidagilarni amalga oshirishi mumkin:

* SMSlarni o‘qish va undan internet-banking yoki ijtimoiy tarmoqlarga kirish uchun foydalanish;
* Joylashuvni aniqlash (bazaviy stansiya koordinatalari orqali);
* Telefon qo‘ng‘iroqlarini tinglash;
* Qurilmani butunlay tarmoqdan uzib qo‘yish.

Bugungi kunda SMS orqali yuboriladigan ikki bosqichli tasdiqlash kodlari (2FA) aynan shu zaiflik sabab xavf ostidadir.

---

### **SS7 hujumlari qanday amalga oshiriladi?**

Umumiy bosqichlar quyidagicha:

1. Faqatgina telefon raqami (MSISDN) bo‘lsa kifoya.
2. Hujumchi SS7ga ulana oladigan uskunani egallaydi (yoki ruxsat oladi).
3. MSISDN orqali IMSI (SIM-karta identifikatori) aniqlanadi.
4. Qo‘ng‘iroq yoki SMS uzatishda marshrut o‘zgartirilib, hujumchi orqali o‘tkaziladi.
5. SMSlar va suhbatlar o‘zlashtiriladi.
6. Xizmatlar bloklanadi yoki qayta yo‘naltiriladi.

---

### **Haqiqiy misollar**

SS7 zaifligi birinchi marta jamoatchilikka 2008-yilda nemis mutaxassisi Tobias Engel tomonidan Chaos Computer Club konferensiyasida ochib berilgan. 2013-yilda Edvard Snouden AQSh maxsus xizmatlari bu protokoldan kuzatuv uchun foydalanganini ma’lum qildi. 2016-yilda esa Karsten Noll Amerikaning “60 Minutes” teleko‘rsatuvida kongressmen Tedd Lyu telefonini jonli efirda “buzib” ko'rsatdi.

---

### **Shunchalik osonmi?**

Yuqoridagilardan so‘ng siz “Telefonimni ham kimdir tinglayaptimi?” deb o‘ylashingiz mumkin. Biroq haqiqatda bunday hujumlarni amalga oshirish juda qiyin:

* SS7 dasturlari ochiq manbada yo‘q va pullik bozorlar (masalan, darknet)dagi takliflar ko‘pincha firibgarlik.
* Malakali mutaxassislar kam va ular bunday ishlarda qatnashishni xohlamaydi.
* Protokolga ulanish uchun operator uskunalariga ruxsat yoki ichki xodim yordam kerak.
* Hujum ochilgan zahoti, operator hujumchini bloklab qo‘yadi.

Bunday hujumlarni asosan maxsus xizmatlar yoki laboratoriya sharoitida operator bilan kelishilgan holda amalga oshirish mumkin.

---

### **Himoya qanday qilinmoqda?**

Operatorlar quyidagi choralarni ko‘rmoqda:

* IMSI ni yashirish yoki vaqtincha identifikatorlar berish;
* SMS yetkazishni o‘z zimmasiga olish;
* 2FA kodlarini SMS orqali emas, autentifikator ilovasi orqali yuborish.

Shuningdek, zamonaviy ikki faktorli himoya usullari (masalan, TOTP) keng qo‘llanilmoqda. Ularda vaqt asosida o‘zgaruvchi kodlar ishlab chiqariladi va ma’lumotlar shifrlanadi.

---

### **Xulosa**

SS7 zaifliklari real tahdid bo‘lishiga qaramasdan, ularning xavfini oshirib ko‘rsatish odatiy hol. Oddiy foydalanuvchi uchun xavf minimal, lekin:

* SMSga bog‘liq ikki faktorli tasdiqlashdan voz keching;
* Faqat ishonchli servis va ilovalardan foydalaning;
* VPN, autentifikator ilovalari, https-saytlardan foydalanishni odat qiling.

**Eng muhimi: xotirjam bo‘ling va texnologiyalardan ongli foydalaning.**

---

Kerak bo'lsa siz buni faqat yaxshilikka ishlating va raxmat aytish shart emas!
