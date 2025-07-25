---
title: Jekyllda ishlashni boshlash
description: Jekyllning Chirpy mavzusi asoslari bilan tanishing. Ushbu
  qo'llanmada siz Jekyllning Chirpy Chirpy asosidagi veb-saytni qanday
  o'rnatish, sozlash va ishlatishni, shuningdek, uni veb-serverga
  joylashtirishni o'rganasiz.
authors:
  - cotes
  - yorenwyl
date: 2025-03-26
categories:
  - Chirpy
  - O'rganish
tags:
  - Chirpy
pin: true
media_subpath: /assets/img/articles/2025-03-26-jekyllda-ishlashni-boshlash
last_modified_at: 2025-07-25
author: yorenwyl
lang: uz-UZ
---
## Sayt Repozitoriyasini Yaratish

Sayt repozitoriyasini yaratishda, ehtiyojlaringizga qarab ikkita variant mavjud:

### Variant 1. Starterdan Foydalanish (Tavsiya etiladi)

Ushbu yondashuv yangilanishlarni soddalashtiradi, keraksiz fayllarni ajratadi va minimal sozlash bilan yozishga e'tibor qaratmoqchi bo'lgan foydalanuvchilar uchun juda mos keladi.

1.  GitHub'ga kiring va [**starter**](https://github.com/cotes2020/chirpy-starter) sahifasiga o'ting.
2.  Use this template tugmasini bosing va keyin Create a new repository ni tanlang.
3.  Yangi repozitoriyani `<username>.github.io` deb nomlang, bu yerda `username` sizning kichik harflardagi GitHub foydalanuvchi nomingiz bilan almashtiriladi.

### Variant 2. Mavzuni Forklash

Ushbu yondashuv xususiyatlarni yoki UI dizaynini o'zgartirish uchun qulay, lekin yangilanishlar paytida qiyinchiliklar tug'diradi. Shuning uchun, agar siz Jekyll bilan tanish bo'lmasangiz va ushbu mavzuni jiddiy o'zgartirishni rejalashtirmasangiz, bu usulni sinab ko'rmang.

1.  GitHub'ga kiring.
2.  [Mavzu repozitoriyasini fork qiling](https://github.com/cotes2020/jekyll-theme-chirpy/fork).
3.  Yangi repozitoriyani `<username>.github.io` deb nomlang, bu yerda `username` sizning kichik harflardagi GitHub foydalanuvchi nomingiz bilan almashtiriladi.

## Muhitni Sozlash

Repozitoriya yaratilgandan so'ng, rivojlanish muhitini sozlash vaqti keldi. Buning ikkita asosiy usuli mavjud:

### Dev Containers'dan Foydalanish (Windows uchun Tavsiya etiladi)

Dev Containers Docker yordamida izolyatsiyalangan muhitni taqdim etadi, bu sizning tizimingiz bilan ziddiyatlarni oldini oladi va barcha bog'liqliklarni konteyner ichida boshqaradi.

**Qadamlar**:

1.  Docker'ni o'rnating:
    *   Windows/macOS'da [Docker Desktop](https://www.docker.com/products/docker-desktop/) ni o'rnating.
    *   Linux'da [Docker Engine](https://docs.docker.com/engine/install/) ni o'rnating.
2.  [VS Code](https://code.visualstudio.com/) va [Dev Containers kengaytmasi](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) ni o'rnating.
3.  Repozitoriyangizni klonlang:
    *   Docker Desktop uchun: VS Code'ni ishga tushiring va [repozitoriyangizni konteyner hajmida klonlang](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume).
    *   Docker Engine uchun: Repozitoriyangizni lokal ravishda klonlang, keyin VS Code orqali [konteynerda oching](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container).
4.  Dev Containers sozlamalari tugashini kuting.

### Mahalliy Sozlash (Unix-like OS uchun Tavsiya etiladi)

Unix-like tizimlar uchun, siz muhitni mahalliy ravishda optimal ishlash uchun sozlashingiz mumkin, lekin Dev Containers'dan alternativ sifatida ham foydalanishingiz mumkin.

**Qadamlar**:

1.  [Jekyll o'rnatish qo'llanmasi](https://jekyllrb.com/docs/installation/) ga amal qilib Jekyll'ni o'rnating va [Git](https://git-scm.com/) o'rnatilganligiga ishonch hosil qiling.
2.  Repozitoriyangizni lokal mashinangizga klonlang.
3.  Agar mavzuni fork qilgan bo'lsangiz, [Node.js](https://nodejs.org/) ni o'rnating va repozitoriyaning root katalogida `bash tools/init.sh` ni ishga tushiring.
4.  Repozitoriyaning root katalogida `bundle` buyrug'ini ishga tushiring va bog'liqliklarni o'rnating.

## Foydalanish

### Jekyll Serverni Ishga Tushirish

Saytni lokal ravishda ishga tushirish uchun quyidagi buyruqdan foydalaning:

```terminal
$ bundle exec jekyll serve
```

### Jekyll Serverda O'zgarishlar Kiritish va Tekshirish

> `Ogohlantirish` Jekyll yordamida saytni lokal serverda ishga tushirganingizda, o'zgarishlarni to'g'ri boshqarish va tekshirish muhimdir! {: .prompt-warning }

Quyida server ishlayotgan paytda o'zgarishlar kiritishdan saqlanish va saytni to'g'ri tekshirish bo'yicha tavsiyalar berilgan.

* * *

#### 1\. **Serverni To'xtatish**

Saytni lokal serverda ishga tushirganingizda, o'zgarishlar kiritishdan oldin serverni to'xtatishingiz kerak. Buning uchun terminalda quyidagi tugmalar kombinatsiyasidan foydalaning:

```terminal
Ctrl + C
```

Bu buyruq serverni to'xtatadi va sizga o'zgarishlarni xavfsiz kiritish imkonini beradi.

* * *

#### 2\. **Saytni Tozalash**

O'zgarishlarni kiritgandan so'ng, Jekyll tomonidan yaratilgan kesh va vaqtinchalik fayllarni tozalash tavsiya etiladi. Buning uchun quyidagi buyruqni ishlating:

```terminal
$ bundle exec jekyll clean
```

Bu buyruq barcha vaqtinchalik fayllarni o'chiradi va saytni toza holatda qayta qurishga tayyorlaydi.

* * *

#### 3\. **Saytni Qayta Ishga Tushirish**

Saytni qayta ishga tushirish uchun quyidagi buyruqdan foydalaning:

```terminal
$ bundle exec jekyll s --incremental --limit_posts 10
```

*   **`--incremental`**: Bu parametr saytni faqat o'zgartirilgan qismlarini qayta quradi, bu esa vaqtni tejaydi.
*   **`--limit_posts 10`**: Bu parametr faqat 10 ta postni yuklaydi, bu esa saytni tezroq ishga tushirishga yordam beradi.

* * *

#### 4\. **Saytni Tekshirish**

Server ishga tushgandan so'ng, saytni lokal serverda quyidagi manzil orqali tekshirishingiz mumkin:

```
http://127.0.0.1:4000
```

Brauzerda saytni ochib, kiritilgan o'zgarishlarni ko'rib chiqing.

* * *

#### 5\. **Tavsiya**

*   Har safar katta o'zgarishlar kiritishdan oldin serverni to'xtatib, saytni tozalashni unutmang.
*   **`--incremental`** parametridan foydalanish saytni tezroq qayta qurishga yordam beradi, lekin katta o'zgarishlar uchun to'liq tozalash va qayta qurish tavsiya etiladi.

Ushbu qadamlar Jekyll bilan ishlashni soddalashtiradi va saytni lokal serverda samarali boshqarishga yordam beradi.

> Agar siz Dev Containers'dan foydalanayotgan bo'lsangiz, bu buyruqni **VS Code** Terminalida ishga tushirishingiz kerak. {: .prompt-info }

Bir necha soniyadan so'ng, lokal server [http://127.0.0.1:4000](http://127.0.0.1:4000) da mavjud bo'ladi.

### Sozlash

`_config.yml`{: .filepath} dagi o'zgaruvchilarni kerakli tarzda yangilang. Ba'zi odatiy variantlar quyidagilarni o'z ichiga oladi:

*   `url`
*   `avatar`
*   `timezone`
*   `lang`

### Ijtimoiy Aloqa Variantlari

Ijtimoiy aloqa variantlari yon panelning pastki qismida ko'rsatiladi. Siz `_data/contact.yml`{: .filepath} faylida ma'lum aloqa variantlarini yoqishingiz yoki o'chirishingiz mumkin.

### Mavzuni Moslashtirish

Mavzuni moslashtirish uchun, mavzuning `assets/css/jekyll-theme-chirpy.scss`{: .filepath} faylini Jekyll saytingizdagi xuddi shu yo'lga nusxalab oling va fayl oxirida o'zingizning maxsus Mavzularingizni qo'shing.

### Statik Aktivlarni Moslashtirish

Statik aktivlar konfiguratsiyasi `5.1.0` versiyasida joriy etilgan. Statik aktivlarning CDN `_data/origin/cors.yml`{: .filepath} da aniqlangan. Siz veb-saytingiz joylashtirilgan hududdagi tarmoq sharoitlariga qarab ularning ba'zilarini almashtirishingiz mumkin.

Agar statik aktivlarni o'zingiz joylashtirishni afzal ko'rsangiz, [_chirpy-static-assets_](https://github.com/cotes2020/chirpy-static-assets#readme) repozitoriyasiga murojaat qiling.

## Joylashtirish

Joylashtirishdan oldin, `_config.yml`{: .filepath} faylini tekshiring va `url` to'g'ri sozlanganligiga ishonch hosil qiling. Agar siz [**loyiha sayti**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) ni afzal ko'rsangiz va maxsus domen ishlatmasangiz yoki GitHub Pages'dan boshqa veb-serverda veb-saytingizga baza URL bilan tashrif buyurmoqchi bo'lsangiz, `baseurl` ni loyihangiz nomiga, masalan, `/project-name` ga o'rnatishni unutmang.

Endi Jekyll saytingizni joylashtirish uchun quyidagi usullardan _BIRINI_ tanlashingiz mumkin.

### GitHub Actions yordamida joylashtirish

Quyidagilarni tayyorlang:

*   Agar siz GitHub Free rejasida bo'lsangiz, sayt repozitoriyangizni ommaviy saqlang.
    
*   Agar `Gemfile.lock`{: .filepath} faylini repozitoriyaga qo'shgan bo'lsangiz va lokal mashinangiz Linuxda ishlamasa, lock faylining platforma ro'yxatini yangilang:
    
    ```console
    $ bundle lock --add-platform x86_64-linux
    ```
    

Keyin _Pages_ xizmatini sozlang:

1.  GitHub'dagi repozitoriyangizga o'ting. _Settings_ yorlig'ini tanlang, so'ng chap navigatsiya panelida _Pages_ ni bosing. **Source** bo'limida ( _Build and deployment_ ostida), ochiladigan menyudan [**GitHub Actions**](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) ni tanlang.  
    ![Build source](pages-source-light.png){: .light .border .normal w='375' h='140' } ![Build source](pages-source-dark.png){: .dark .normal w='375' h='140' }
    
2.  Har qanday commitni GitHub'ga yuboring, bu _Actions_ ish jarayonini ishga tushiradi. Repozitoriyaning _Actions_ yorlig'ida _Build and Deploy_ ish jarayonini ko'rishingiz kerak. Qurilish tugallangandan va muvaffaqiyatli bo'lgandan so'ng, sayt avtomatik ravishda joylashtiriladi.
    

Endi saytga kirish uchun GitHub tomonidan taqdim etilgan URL manziliga tashrif buyurishingiz mumkin.

### Qo'lda Qurish va Joylashtirish

O'zingiz joylashtirgan serverlar uchun, saytni lokal mashinangizda qurishingiz va keyin sayt fayllarini serverga yuklashingiz kerak bo'ladi.

Loyiha manbasi root katalogiga o'ting va saytni quyidagi buyruq bilan qurib chiqing:

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

Agar chiqish yo'lini belgilamagan bo'lsangiz, yaratilgan sayt fayllari loyiha root katalogidagi `_site`{: .filepath} papkasiga joylashtiriladi. Ushbu fayllarni maqsadli serverga yuklang.