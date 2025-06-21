---
title: clean bash
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichida qilgan ba'zi ishlarim aks ettirilgan.
author: yorenwyl
date: 2025-06-21 14:51:00 +0500
categories: [21-IT Maktab - School 21, Basseyn - C Piscine]
tags: [Basseyn - C Piscine]
pin: true
image:
  path: /clean.gif
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 21-IT Maktab - School 21.
media_subpath: "/assets/img/articles/2025-03-26-basseynga-tayyorlanish/"
---

Quyida sizga **foydalanuvchi keshlarini, brauzer va VS Code qoldiqlarini, trash fayllarini avtomatik tozalovchi bash skript** keltirilgan.

---

## 🧹 `clean_user_cache.sh` — avtomatik tozalovchi skript

```bash
#!/bin/bash

echo "🧹 Foydalanuvchi kesh va vaqtinchalik fayllarni tozalash boshlandi..."

# 1. Trash
echo " - Trash fayllari tozalanmoqda..."
rm -rf ~/.local/share/Trash/*

# 2. Umumiy cache
echo " - ~/.cache tozalanmoqda..."
rm -rf ~/.cache/*

# 3. VS Code keshlari
echo " - VS Code cache tozalanmoqda..."
rm -rf ~/.config/Code/Cache/*
rm -rf ~/.config/Code/CachedData/*
rm -rf ~/.config/Code/Code\ Cache/*
rm -rf ~/.config/Code/GPUCache/*
rm -rf ~/.config/Code/logs/*

# 4. Google Chrome kesh
echo " - Chrome cache tozalanmoqda..."
rm -rf ~/.config/google-chrome/ShaderCache/*
rm -rf ~/.config/google-chrome/Crash\ Reports/*
rm -rf ~/.config/google-chrome/GrShaderCache/*
rm -rf ~/.config/google-chrome/component_crx_cache/*
rm -rf ~/.config/google-chrome/extensions_crx_cache/*
rm -rf ~/.config/google-chrome/OptimizationHints/*
rm -rf ~/.config/google-chrome/Webstore\ Downloads/*

# 5. KDE thumbnail va plasmashell cache
echo " - KDE thumbnails va plasmashell qoldiqlari tozalanmoqda..."
rm -rf ~/.cache/plasmashell/qmlcache/*
rm -rf ~/.cache/thumbnails/*
rm -rf ~/.cache/ksycoca5_*
rm -rf ~/.config/session/*
rm -rf ~/.cache/mesa_shader_cache/*

echo "✅ Tozalash tugadi."
```

---

## 💾 Foydalanish:

1. Faylga saqlang:

   ```bash
   nano clean_user_cache.sh
   ```

   (yoki `touch` va `echo`, yoki VS Code’da)

2. Ruxsat bering:

   ```bash
   chmod +x clean_user_cache.sh
   ```

3. Ishga tushiring:

   ```bash
   ./clean_user_cache.sh
   ```

---

## ⏱ Avtomatlashtirish (ixtiyoriy)

Agar siz har ishga tushganda yoki haftada bir tozalashni xohlasangiz:

* `cron` (jadval asosida)
* yoki `.bashrc` / `.zshrc` oxiriga:

```bash
# clear every login
# bash ~/scripts/clean_user_cache.sh
```

---
