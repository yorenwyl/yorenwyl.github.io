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

```bash
#include "evaluate_rpn.h" // evaluate_rpn.h sarlavha faylini ulaydi; funktsiyalar prototiplarini o'z ichiga oladi. Kutubxona: yo'q (foydalanuvchi tomonidan yaratilgan).

char *ftos(double num) { // double sonni stringga aylantiruvchi funksiya e'lon qiladi. Kutubxona: yo'q.
    char *str = (char *)malloc(20); // 20 bayt xotira ajratadi va string uchun ko'rsatkich yaratadi. Kutubxona: stdlib.h (malloc).
    snprintf(str, 20, "%lf", num); // double sonni formatlab stringga yozadi. Kutubxona: stdio.h (snprintf).
    return str; // String ko'rsatkichini qaytaradi. Kutubxona: yo'q.
} // Funksiya yakunlanadi. Kutubxona: yo'q.

void function_variable(const Token *current_token, Stack *operand_stack, double x) { // O'zgaruvchi bilan ishlovchi funksiya; token, stack va x qiymatini qabul qiladi. Kutubxona: yo'q.
    if (current_token->value[0] == '-') { // Tokenning birinchi belgisi minus ekanligini tekshiradi. Kutubxona: yo'q.
        char *ccc = ftos(-x); // x ning manfiy qiymatini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Stringni stackka qo'shadi. Kutubxona: yo'q (stack.h dan stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else { // Agar token minus bilan boshlanmasa. Kutubxona: yo'q.
        char *ccc = ftos(x); // x qiymatini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Stringni stackka qo'shadi. Kutubxona: yo'q (stack.h dan stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } // Shartli operator yakunlanadi. Kutubxona: yo'q.
} // Funksiya yakunlanadi. Kutubxona: yo'q.

void function_operator(const Token *current_token, Stack *operand_stack) { // Operatorlar bilan ishlovchi funksiya; token va stackni qabul qiladi. Kutubxona: yo'q.
    double operand2 = atof(stack_top(operand_stack)); // Stackning yuqori elementini o'qib, uni double ga aylantiradi. Kutubxona: stdlib.h (atof), stack.h (stack_top).
    char *o1 = stack_pop(operand_stack); // Stackdan yuqori elementni oladi va o'chiradi. Kutubxona: stack.h (stack_pop).
    free(o1); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    double operand1 = atof(stack_top(operand_stack)); // Stackning yangi yuqori elementini double ga aylantiradi. Kutubxona: stdlib.h (atof), stack.h (stack_top).
    char *o2 = stack_pop(operand_stack); // Stackdan yangi yuqori elementni oladi va o'chiradi. Kutubxona: stack.h (stack_pop).
    free(o2); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).

    if (strcmp(current_token->value, "+") == 0) { // Token qiymati "+" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(operand1 + operand2); // Operandlar yig'indisini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "-") == 0) { // Token qiymati "-" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(operand1 - operand2); // Operandlar ayirmasini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "*") == 0) { // Token qiymati "*" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(operand1 * operand2); // Operandlar ko'paytmasini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "/") == 0) { // Token qiymati "/" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(operand1 / operand2); // Operandlar bo'linmasini stringga aylantiradi. Kutubxona: yo'q (ftos foydalanuvchi funksiyasi).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } // Shartli operator yakunlanadi. Kutubxona: yo'q.
} // Funksiya yakunlanadi. Kutubxona: yo'q.

void function_function(const Token *current_token, Stack *operand_stack) { // Matematik funksiyalar bilan ishlovchi funksiya; token va stackni qabul qiladi. Kutubxona: yo'q.
    double operand = atof(stack_top(operand_stack)); // Stackning yuqori elementini double ga aylantiradi. Kutubxona: stdlib.h (atof), stack.h (stack_top).
    char *c = stack_pop(operand_stack); // Stackdan yuqori elementni oladi va o'chiradi. Kutubxona: stack.h (stack_pop).
    free(c); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).

    if (strcmp(current_token->value, "sin") == 0) { // Token qiymati "sin" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(sin(operand)); // Operandning sinusini hisoblaydi va stringga aylantiradi. Kutubxona: math.h (sin), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "cos") == 0) { // Token qiymati "cos" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(cos(operand)); // Operandning kosinusini hisoblaydi va stringga aylantiradi. Kutubxona: math.h (cos), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "tan") == 0) { // Token qiymati "tan" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(tan(operand)); // Operandning tangensini hisoblaydi va stringga aylantiradi. Kutubxona: math.h (tan), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "ctg") == 0) { // Token qiymati "ctg" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(1.0 / tan(operand)); // Operandning kotangensini (1/tan) hisoblaydi va stringga aylantiradi. Kutubxona: math.h (tan), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "sqrt") == 0) { // Token qiymati "sqrt" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(sqrt(operand)); // Operandning kvadrat ildizini hisoblaydi va stringga aylantiradi. Kutubxona: math.h (sqrt), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } else if (strcmp(current_token->value, "ln") == 0) { // Token qiymati "ln" ekanligini tekshiradi. Kutubxona: string.h (strcmp).
        char *ccc = ftos(log(operand)); // Operandning natural logarifmini hisoblaydi va stringga aylantiradi. Kutubxona: math.h (log), yo'q (ftos).
        stack_push(operand_stack, ccc); // Natijani stackka qo'shadi. Kutubxona: stack.h (stack_push).
        free(ccc); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).
    } // Shartli operator yakunlanadi. Kutubxona: yo'q.
} // Funksiya yakunlanadi. Kutubxona: yo'q.

double evaluate_rpn(const Token *rpn_tokens, int num_rpn_tokens, double x) { // RPN ifodasini hisoblovchi funksiya; tokenlar, ular soni va x qiymatini qabul qiladi. Kutubxona: yo'q.
    Stack operand_stack; // Operandlar uchun stack o'zgaruvchisini e'lon qiladi. Kutubxona: stack.h (Stack).
    stack_init(&operand_stack, num_rpn_tokens); // Stackni boshlaydi va unga xotira ajratadi. Kutubxona: stack.h (stack_init).

    for (int i = 0; i < num_rpn_tokens; i++) { // Tokenlar bo'yicha sikl boshlaydi. Kutubxona: yo'q.
        const Token *current_token = &rpn_tokens[i]; // Joriy tokenni o'zgaruvchiga saqlaydi. Kutubxona: yo'q.
        if (current_token->type == TOKEN_NUMBER) { // Token turi son ekanligini tekshiradi. Kutubxona: yo'q.
            stack_push(&operand_stack, current_token->value); // Son qiymatini stackka qo'shadi. Kutubxona: stack.h (stack_push).
        } else if (current_token->type == TOKEN_VARIABLE) { // Token turi o'zgaruvchi ekanligini tekshiradi. Kutubxona: yo'q.
            function_variable(current_token, &operand_stack, x); // O'zgaruvchi bilan ishlovchi funksiyani chaqiradi. Kutubxona: yo'q (function_variable).
        } else if (current_token->type == TOKEN_OPERATOR) { // Token turi operator ekanligini tekshiradi. Kutubxona: yo'q.
            function_operator(current_token, &operand_stack); // Operator bilan ishlovchi funksiyani chaqiradi. Kutubxona: yo'q (function_operator).
        } else if (current_token->type == TOKEN_FUNCTION) { // Token turi funksiya ekanligini tekshiradi. Kutubxona: yo'q.
            function_function(current_token, &operand_stack); // Matematik funksiya bilan ishlovchi funksiyani chaqiradi. Kutubxona: yo'q (function_function).
        } // Shartli operator yakunlanadi. Kutubxona: yo'q.
    } // Sikl yakunlanadi. Kutubxona: yo'q.

    double result = atof(stack_top(&operand_stack)); // Stackning yuqori elementini double ga aylantirib, natija sifatida saqlaydi. Kutubxona: stdlib.h (atof), stack.h (stack_top).
    char *c = stack_pop(&operand_stack); // Stackdan yuqori elementni oladi va o'chiradi. Kutubxona: stack.h (stack_pop).
    free(c); // Ajratilgan xotirani bo'shatadi. Kutubxona: stdlib.h (free).

    stack_free(&operand_stack); // Stackdagi barcha xotirani bo'shatadi. Kutubxona: stack.h (stack_free).
    return result; // Hisoblangan natijani qaytaradi. Kutubxona: yo'q.
} // Funksiya yakunlanadi. Kutubxona: yo'q.

double evaluate_rpn_function(const Token *rpn_tokens, int num_rpn_tokens, double x) { // evaluate_rpn funksiyasini qayta chaqiruvchi yordamchi funksiya. Kutubxona: yo'q.
    return evaluate_rpn(rpn_tokens, num_rpn_tokens, x); // evaluate_rpn funksiyasini chaqirib, natijani qaytaradi. Kutubxona: yo'q (evaluate_rpn).
} // Funksiya yakunlanadi. Kutubxona: yo'q.
```
