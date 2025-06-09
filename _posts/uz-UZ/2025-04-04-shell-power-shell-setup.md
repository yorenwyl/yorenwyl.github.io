---
title: "Takuya Matsuyama: PowerShell'ni sanʼat darajasida sozlash"
date: 2025-04-05 12:00:00 +0500
categories: [Productivity, Terminal]
tags: [PowerShell, Takuya, dotfiles, terminal, Windows, Devaslife]
description: PowerShellni sozlash
author: yorenwyl
---

# "Takuya Matsuyama: PowerShell'ni sanʼat darajasida sozlash"
---

Dasturchilar orasida minimalizm va estetikani birlashtira olgan kam sonli insonlar bor. Ulardan biri — **Takuya Matsuyama**, [Devaslife](https://www.youtube.com/@devaslife){: target="_blank" } va [craftzdog](https://www.youtube.com/@craftzdog){: target="_blank" } YouTube kanallari muallifi. U dasturlash muhiti, terminal va ish jarayonini mukammallikka yetkazgan odamlardan.

Bu postda Takuya tomonidan PowerShell’ni qanday qilib yuqori darajada sozlash mumkinligi, foydalanilgan vositalar va kerakli manbalar haqida so‘z yuritamiz.

---

## 🎯 Nima uchun PowerShell?

Takuya avval Linux/MacOS’dagi **Zsh** terminalidan foydalangan, biroq Windows foydalanuvchilari uchun ham xuddi shunday samarali va estetik terminal yaratish maqsadida PowerShell'ga eʼtibor qaratdi. U Windows Terminal bilan uyg‘un holda ishlaydigan, tezkor va qulay terminal muhitini ishlab chiqdi.

---

## ⚙️ Asosiy vositalar

Takuya PowerShell muhiti uchun quyidagi vositalardan foydalangan:

| Vosita | Tavsifi |
|--------|---------|
| [Oh My Posh](https://ohmyposh.dev/){: target="_blank" } | Terminal prompt dizaynini sozlash uchun |
| Cascadia Code PL | Powerline belgilarni qo‘llab-quvvatlaydigan shrift |
| Windows Terminal | Terminal interfeysi uchun zamonaviy vosita |
| [PSReadLine](https://github.com/PowerShell/PSReadLine){: target="_blank" } | Intuitiv klaviatura qo‘llab-quvvatlovi |
| `z` | Oxirgi ishlatilgan kataloglarga tez o‘tish |
| [fzf](https://github.com/junegunn/fzf){: target="_blank" } | Interaktiv fayl qidiruv vositasi |

---

## 🧰 Dotfiles: Takuya sozlamalari

Takuya o‘zining barcha konfiguratsiyalarini **GitHub**'da ochiq holda ulashgan:

🔗 **Dotfiles repozitoriyasi:**  
👉 [github.com/craftzdog/dotfiles-public](https://github.com/craftzdog/dotfiles-public){: target="_blank" }

Unda quyidagilarni topasiz:

- PowerShell profillari
- Oh My Posh konfiguratsiyasi
- Windows Terminal sozlamalari
- Neovim konfiguratsiyasi (bonus!)

# Klonlash:
```bash
git clone https://github.com/craftzdog/dotfiles-public.git
```

---

## 📺 YouTube video: PowerShell Setup

PowerShell muhitini qanday qilib chiroyli va samarali sozlashni Takuya quyidagi videosida batafsil tushuntirgan:

{% include embed/youtube.html id='5-aK2_WwrmM' %}

🎬 Video mazmuni:
- Windows Terminal uchun profil yaratish
- Cascadia Code PL shriftini o‘rnatish
- Oh My Posh bilan prompt bezatish
- Modul o‘rnatish va import qilish
- PowerShell profil faylini yozish

---

## 🔌 Modul o‘rnatish (praktik buyruqlar)

## Oh My Posh
```powershell
Install-Module -Name oh-my-posh -Scope CurrentUser
```
## PSReadLine
```powershell
Install-Module -Name PSReadLine -Force -SkipPublisherCheck
```

## z - tezkor papkaga o'tish
```powershell
Install-Module -Name z -AllowClobber
```

**Profil fayli (`Microsoft.PowerShell_profile.ps1`)** quyidagi faylga yoziladi:
```powershell
notepad $PROFILE
```

---

## ✨ Yakuniy mulohaza

Takuya Matsuyama terminalni oddiy ish quroli emas, balki ilhomlantiruvchi sanʼat asariga aylantira olgan. U nafaqat texnik jihatdan mukammal konfiguratsiyalarni yaratgan, balki uni ommaga ochiq qilib, ko‘pchilikka yordam bermoqda.

Agar siz ham PowerShell’ni chiroyli va qulay terminalga aylantirmoqchi bo‘lsangiz — **Takuya dotfiles** va **videosidan** ilhom oling!

---

**Foydali havolalar:**

- 🔗 [Takuya GitHub: craftzdog](https://github.com/craftzdog){: target="_blank" }
- 📺 [Devaslife YouTube](https://www.youtube.com/@devaslife){: target="_blank" }
- 📺 [craftzdog YouTube](https://www.youtube.com/@craftzdog){: target="_blank" }
- 🧑‍💻 [Dotfiles repository](https://github.com/craftzdog/dotfiles-public){: target="_blank" }
