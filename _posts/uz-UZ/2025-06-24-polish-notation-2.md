---
title: Polish notation bilan ishlash
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichiga tayyorlanish uchun mo‘ljallangan, bajarilgan va izohlangan vazifalarning turli versiyalari taqdim etilgan.
author: yorenwyl
date: 2025-06-24 18:02:00 +0500
categories: [21-IT Maktab - School 21, Basseyn - C Piscine]
tags: [Basseyn - C Piscine]
pin: true
image:
  path: /sinx.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 21-IT Maktab - School 21.
media_subpath: "/assets/img/articles/2025-03-26-basseynga-tayyorlanish/"
---

---

## **Basseyn(С piscine)ga tayyorlanish uchun zarur manbalar** 

> Siz dastlabki testdan o'tib zarur xujjatlarni maktabga topshirgach sizga basseynga qadar bo'lgan vaqtda tayyorlanishingiz uchun kitoblar ro'yxati junatiladi.
{: .prompt-tip }

[🔄 Sahifani yangilash](javascript:location.reload()){:.shadow}

<details>
      <summary>📕 O‘RGANISH UCHUN RESURSLAR </summary>
      // Bu yerga kod to'liq izoxlar bilan yozildi
</details>

# Reverse Polish Notation (RPN) Kalkulyatori: Matematik Ifodalarni Qayta Ishlash Loyihasi

Ushbu maqolada men yaratgan Reverse Polish Notation (RPN) kalkulyatori loyihasi haqida so'zlab o'taman. Loyiha C dasturlash tilida yozilgan bo'lib, matematik ifodalarni qayta ishlash va ularni grafik ko'rinishda tasvirlash imkonini beradi.

## Loyiha Tarkibi

Loyiha quyidagi asosiy komponentlardan iborat:

1. **Matematik ifodalarni tahlil qilish (parsing)**
2. **Infix notatsiyadan RPN ga o'tkazish**
3. **RPN ifodasini baholash**
4. **Natijani grafik ko'rinishda tasvirlash**

### Asosiy Fayllar

```bash
.
├── evaluate_rpn.[c/h]      - RPN ifodasini baholash
├── infix_to_rpn.[c/h]      - Infix dan RPN ga o'tkazish
├── parse_expression.[c/h]  - Ifodalarni tahlil qilish
├── rendering_image.[c/h]   - Grafik tasvir
├── stack.[c/h]             - Stack amallari
├── token.h                 - Token turlari
└── graph.c                 - Asosiy dastur
```

## Qiziqarli Imkoniyatlar

### 1. Matematik Ifodalarni Qo'llab-quvvatlash

Dastur quyidagi matematik operatsiyalarni qo'llab-quvvatlaydi:
- Asosiy arifmetik amallar: `+`, `-`, `*`, `/`
- Trigonometrik funksiyalar: `sin`, `cos`, `tan`, `ctg`
- Boshqa funksiyalar: `sqrt`, `ln`
- Unary minus (`-5` kabi ifodalar)

### 2. Grafik Tasvir

Dastur 80x25 o'lchamdagi matritsa yordamida funksiya grafigini chizadi. Misol uchun, `sin(x)` funksiyasi uchun:

```

## Texnik Tafsilotlar

### Token Turlari

```c
typedef enum {
    TOKEN_NUMBER,      // sonlar
    TOKEN_OPERATOR,    // matematik operatorlar
    TOKEN_FUNCTION,    // matematik funksiyalar
    TOKEN_VARIABLE,    // o'zgaruvchilar (x)
    TOKEN_LEFT_PAREN,  // ochuvchi qavs
    TOKEN_RIGHT_PAREN  // yopuvchi qavs
} TokenType;
```

### Stack Amallari

Loyihada RPN algoritmini amalga oshirish uchun stack (stek) ma'lumotlar tuzilmasi qo'llanilgan:

```c
typedef struct {
    char **data;
    int size;
    int top;
} Stack;

void stack_init(Stack *stack, int size);
int stack_empty(const Stack *stack);
void stack_push(Stack *stack, const char *value);
char *stack_pop(Stack *stack);
char *stack_top(const Stack *stack);
void stack_free(Stack *stack);
```

### Asosiy Algoritmlar

1. **Ifodalarni tahlil qilish** - `parse_expression.c`
2. **Infix dan RPN ga o'tkazish** - Shunting-yard algoritmi, `infix_to_rpn.c`
3. **RPN ni baholash** - `evaluate_rpn.c`
4. **Grafik chizish** - `rendering_image.c`

## Loyihani Ishlatish

Loyihani ishga tushirish uchun:

```bash
make all
make run
```

Keyin sizdan matematik ifoda kiritish so'raladi, masalan: `sin(x) + cos(x)`

## Xulosa

Ushbu loyiha orqali men:
- Matematik ifodalarni tahlil qilish va ularni RPN ko'rinishiga o'tkazishni o'rgandim
- Stack ma'lumotlar tuzilmasini amaliy loyihada qo'lladim
- C tilida modulli dasturlash tamoyillarini qo'lladim
- Grafik tasvirlash algoritmlari bilan ishlash tajribasini orttirdim

Loyiha kodini to'liq ko'rish uchun mening GitHub profilimga tashrif buyurishingiz mumkin.

---
