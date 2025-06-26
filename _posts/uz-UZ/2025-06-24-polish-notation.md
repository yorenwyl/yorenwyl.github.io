---
title: Polish notation bilan ishlash
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichiga tayyorlanish uchun mo‘ljallangan, bajarilgan va izohlangan vazifalarning turli versiyalari taqdim etilgan.
author: yorenwyl
date: 2025-06-24 18:02:00 +0500
categories: [21-IT Maktab - School 21, Basseyn - C Piscine]
tags: [Basseyn - C Piscine]
pin: true
image:
  path: /rpn.gif
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 21-IT Maktab - School 21.
media_subpath: "/assets/img/articles/2025-03-26-basseynga-tayyorlanish/"
---

---

## **Polish notation** 

> Ushbu maqolada "Polish notation" bilan ishlash haqida gap ketadi.
{: .prompt-tip }

---

## 🧮 Reverse Polish Notation (RPN) Kalkulyatori Tarixi

### 📌 RPN nima?

**Reverse Polish Notation (RPN)** – bu matematik ifodalarni yozish usuli bo‘lib, unda **amal operatorlari operandlardan keyin** yoziladi. Masalan:

* An’anaviy: `3 + 4`
* RPN: `3 4 +`

Bu usulda qavslar kerak emas – amallar bajarilish tartibi operandlar va operatorlar joylashuviga qarab aniqlanadi.

---

### 🧠 Tarixiy kelib chiqishi

#### 🇵🇱 Jan Łukasiewicz (1920-yillar)

RPN **polshalik mantiqshunos** **Jan Łukasiewicz** tomonidan ishlab chiqilgan **Polish Notation (PN)** g‘oyasidan kelib chiqqan. U algebraik ifodalarni kompyuterlar uchun sodda formatda ifodalash yo‘llarini izlagan.

* **PN (Polish Notation)**: operator **oldinda** (`+ 3 4`)
* **RPN (Reverse Polish Notation)**: operator **orqada** (`3 4 +`)

---

### 🖥️ Kompyuter va RPN

#### 1950–60-yillar: Ilk RPN modellar

RPN ilk bor kompyuter tillarida **stack-based** (stack asosli) hisoblashlarni soddalashtirish uchun qo‘llanilgan. Ayniqsa, **postfix** format kompyuterda ifodalarni **qavsiz** tahlil qilishni osonlashtirgan.

#### 1963: **Burroughs B5000** protsessori

Burroughs kompaniyasi ishlab chiqqan B5000 kompyuteri RPN printsipiga asoslangan **stack-based arxitekturani** birinchi marta apparat darajasida qo‘llagan.

---

### 📟 RPN kalkulyatorlarining paydo bo‘lishi

#### 🔬 HP (Hewlett-Packard) – RPN ni mashhur qilgan kompaniya

* **1972**: HP kompaniyasi **HP-35** nomli ilk ilmiy kalkulyatorni taqdim etdi – bu **dunyoning birinchi RPN kalkulyatori** edi.
* HP kalkulyatorlari stack asosida ishlaydi: har bir raqam stack’ga qo‘shiladi, operator esa stack’dagi qiymatlarni ishlatadi.

#### HP-11C, HP-15C, HP-48 va boshqalar

80–90-yillarda ishlab chiqarilgan ko‘plab professional kalkulyatorlar (muhandislar, fiziklar, matematiklar uchun) RPN formatidan foydalangan.

---

### ✅ RPN afzalliklari

* Qavslar kerak emas
* Amallar bajarilish tartibi aniqligi
* Stack bilan to‘g‘ridan-to‘g‘ri ishlash imkoniyati
* Hisoblash jarayoni sodda va izchil

---

### ❌ Kamchiliklari

* Yangi foydalanuvchilar uchun g‘ayritabiiy ko‘rinadi
* Mashq talab qiladi
* An’anaviy yozuvga o‘xshamaydi

---

### 📱 Bugungi holat

Hozirda ko‘pchilik kalkulyatorlar klassik algebraik (infix) sintaksisdan foydalansa ham, **RPN kalkulyatorlar** hanuzgacha **professional foydalanuvchilar orasida mashhur**. HP, SwissMicros va ba’zi mobil ilovalar hali ham RPN ni qo‘llab-quvvatlaydi.

---

## 🏁 Xulosa

Reverse Polish Notation — bu matematik ifodalarni kompyuterlar uchun qulay va samarali tarzda ifodalash usuli bo‘lib, uning ildizlari XX asr boshidagi mantiqiy tadqiqotlarga borib taqaladi. HP kalkulyatorlari orqali mashhurlikka erishgan bu metod bugungi kunda ham texnik va ilmiy sohalarda o‘z o‘rnini saqlab qolgan.

---

> Men yasagan "Polish notation" bilan ishlash zarur bo'lgan gurux ishi kodini C dasturlash tilida ushbu ma'qolada sizga taqdim etaman.
{: .prompt-tip }

### Asosiy Fayllar
# Matematik Ifodalarni Tahlil Qilish va Grafik Ko'rsatish Dasturi

Ushbu maqolada men yozgan C dasturi haqida batafsil ma'lumot beraman. Dastur matematik ifodalarni qabul qilib, ularni tahlil qiladi, Reverse Polish Notation (RPN) shakliga o'tkazadi va natijani grafik ko'rinishda konsolga chiqaradi.

## Dastur Tuzilishi

Dastur quyidagi modullardan iborat:

1. **parse_expression** - matn shaklidagi matematik ifodani tokenlarga ajratadi
2. **infix_to_rpn** - infix notatsiyadagi ifodani RPN (postfix) ga o'tkazadi
3. **evaluate_rpn** - RPN ifodasini hisoblaydi
4. **rendering_image** - hisoblash natijalarini grafik shaklda ko'rsatadi
5. **stack** - stack ma'lumotlar strukturasi va uning operatsiyalari
6. **token** - token turlari va strukturasi

## Asosiy Funksiyalar

### 1. Ifodani Tahlil Qilish (parse_expression.c)

Bu modul foydalanuvchi kiritgan matnli ifodani quyidagi token turlariga ajratadi:

- Sonlar (TOKEN_NUMBER)
- Operatorlar (TOKEN_OPERATOR: +, -, *, /)
- Funktsiyalar (TOKEN_FUNCTION: sin, cos, tan, ctg, sqrt, ln)
- O'zgaruvchilar (TOKEN_VARIABLE: x)
- Qavslar (TOKEN_LEFT_PAREN, TOKEN_RIGHT_PAREN)

```c
void parse_expression(const char *expression, Token **tokens, int *num_tokens) {
    *num_tokens = 0;
    *tokens = NULL;
    int i = 0;
    while (expression[i] != '\0') {
        if (expression[i] == ' ') {
            i++;
            continue;
        }
        if (my_isdigit(expression[i])) {
            processing_numbers(expression, tokens, num_tokens, &i);
        } else if (expression[i] == '-' && ... ) {
            unary_minus(tokens, num_tokens, &i);
        } else if (is_operator(expression[i])) {
            processing_operators(expression, tokens, num_tokens, &i);
        }
        // ... boshqa token turlari
    }
}
```

### 2. Infixdan RPN ga O'tkazish (infix_to_rpn.c)

Bu modul infix notatsiyadagi ifodani (masalan, "3 + 4 * 2") postfix (RPN) shakliga ("3 4 2 * +") o'tkazadi. Bunda Shunting-yard algoritmi qo'llaniladi.

```c
void infix_to_rpn(const Token *infix_tokens, int num_infix_tokens, Token **rpn_tokens, int *num_rpn_tokens) {
    *num_rpn_tokens = 0;
    *rpn_tokens = NULL;
    Stack operator_stack;
    stack_init(&operator_stack, num_infix_tokens);

    for (int i = 0; i < num_infix_tokens; i++) {
        const Token *current_token = &infix_tokens[i];
        if (current_token->type == TOKEN_NUMBER || current_token->type == TOKEN_VARIABLE) {
            number_or_variable(rpn_tokens, num_rpn_tokens, current_token);
        }
        // ... boshqa token turlarini qayta ishlash
    }
    // ... stackda qolgan operatorlarni chiqarish
}
```

### 3. RPN Ifodasini Hisoblash (evaluate_rpn.c)

Bu modul RPN shaklidagi ifodani hisoblab, natijani qaytaradi. Bunda stackdan foydalaniladi.

```c
double evaluate_rpn(const Token *rpn_tokens, int num_rpn_tokens, double x) {
    Stack operand_stack;
    stack_init(&operand_stack, num_rpn_tokens);

    for (int i = 0; i < num_rpn_tokens; i++) {
        const Token *current_token = &rpn_tokens[i];
        if (current_token->type == TOKEN_NUMBER) {
            stack_push(&operand_stack, current_token->value);
        } else if (current_token->type == TOKEN_VARIABLE) {
            function_variable(current_token, &operand_stack, x);
        }
        // ... boshqa token turlarini qayta ishlash
    }
    // ... natijani olish va stackni tozalash
}
```

### 4. Grafik Tasvirni Yaratish (rendering_image.c)

Bu modul hisoblash natijalarini 25x80 o'lchamdagi matritsaga joylashtirib, konsolga chiqaradi.

```c
void create_graphic(int matrix[HEIGHT][WIDTH], const Token *rpn_tokens, int num_rpn_tokens) {
    for (int i = 0; i < WIDTH; i++) {
        double x = (i * 4.0 * M_PI) / (WIDTH - 1);
        double res = evaluate_rpn_function(rpn_tokens, num_rpn_tokens, x);
        int y = round((res + 1) * (HEIGHT - 1) / 2);
        if (y >= 0 && y < HEIGHT) {
            matrix[y][i] = sym;
        }
    }
}
```

## Stack Implementatsiyasi (stack.c)

Dasturda stack ma'lumotlar strukturasi tokenlarni saqlash va RPN ga o'tkazish jarayonida qo'llaniladi.

```c
void stack_init(Stack *stack, int size) {
    stack->data = (char **)malloc(sizeof(char *) * size);
    stack->size = size;
    stack->top = -1;
}

void stack_push(Stack *stack, const char *value) {
    if (stack->top < stack->size - 1) {
        stack->top++;
        stack->data[stack->top] = (char *)malloc(sizeof(char) * (strlen(value) + 1));
        strcpy(stack->data[stack->top], value);
    }
}
```

## Token Turlari (token.h)

Dasturdagi barcha token turlari quyidagi enum orqali belgilanadi:

```c
typedef enum {
    TOKEN_NUMBER,      // sonlar
    TOKEN_OPERATOR,    // +, -, *, /
    TOKEN_FUNCTION,    // sin, cos, tan, ctg, sqrt, ln
    TOKEN_VARIABLE,    // x
    TOKEN_LEFT_PAREN,  // (
    TOKEN_RIGHT_PAREN  // )
} TokenType;
```

## Dasturdan Foydalanish

Quyidagi `Makefile` — C dasturlash loyihasini avtomatik tarzda tuzish (build), tozalash (clean), formatlash (clang-format), tahlil qilish (cppcheck), va ishga tushirish (run) imkonini beruvchi avtomatlashtirilgan skript hisoblanadi. Quyida har bir qator va bo‘limni sodda qilib tushuntirib beraman:

---

## 🔧 Asosiy sozlamalar:

```make
CC = gcc
CFLAGS = -c -Wall -Werror -Wextra
```

* `CC` – kompilyator nomi (`gcc`).
* `CFLAGS` – kompilyatsiya bayroqlari:

  * `-c` → faqat obyekt (.o) fayl yaratadi.
  * `-Wall` → barcha ogohlantirishlarni ko‘rsatadi.
  * `-Werror` → ogohlantirishlarni xatoga aylantiradi.
  * `-Wextra` → qo‘shimcha ogohlantirishlar.

---

## 📄 Manba fayllar:

```make
SRC1 = graph.c
SRC2 = evaluate_rpn.c
...
SRC6 = stack.c
```

* Har bir `.c` fayl — alohida modulni ifodalaydi.

---

## 🔁 Obyekt fayl nomlari:

```make
OBJ1=$(patsubst %.c,%,$(SRC1))
...
OBJ6=$(patsubst %.c,%,$(SRC6))
```

* Har bir `.c` fayldan nomini olib `.o` faylga mos nomlar hosil qiladi (`graph.c → graph_q.o` bo‘ladi keyinchalik).

---

## 📁 Kataloglar:

```make
BUILD = ../build
SRC_DIR = .
Q = $(BUILD)/graph
```

* `BUILD` → tayyor dastur saqlanadigan papka.
* `SRC_DIR` → manba kodlar joylashgan papka.
* `Q` → yakuniy bajariluvchi fayl (`../build/graph`).

---

## 🧱 `all` – Loyihani tuzish:

```make
all: ..._q.o ...
    @mkdir -p $(BUILD)
    $(CC) $^ -o $(Q) -lm
```

* Barcha `.o` fayllarni kompilyatsiya qiladi.
* `mkdir -p` → `build` papkasini yaratadi (agar mavjud bo‘lmasa).
* `$^` → barcha `.o` fayllar ro‘yxati.
* `-lm` → `math.h` funksiyalari uchun matematik kutubxona.

---

## ⚙️ Har bir `.o` faylni kompilyatsiya qilish:

```make
$(OBJ1)_q.o: $(SRC1)
    $(CC) $(CFLAGS) $^ -o $@
```

* `graph.c` → `graph_q.o` ni yaratadi.
* `$^` → kerakli `.c` fayl.
* `$@` → chiqadigan obyekt fayl nomi.

---

## 🧹 Tozalash buyruqlari:

```make
clean:
    rm -f *.o
    [ -d $(BUILD) ] && find $(BUILD) -type f -not -name '.gitkeep' -delete || true
```

* `clean` → `.o` fayllar va `build/` ichidagi fayllarni o‘chiradi (`.gitkeep`dan tashqari).

```make
clean_outs:
    rm -f *.o
```

* Faqat `.o` fayllarni o‘chiradi.

---

## ♻️ Qayta tuzish:

```make
rebuild: clean all
```

* Dastlab tozalaydi, keyin yangidan tuzadi.

---

## ✅ Cppcheck – statik tahlil vositasi:

```make
cppcheck:
    cppcheck --enable=all --suppress=missingIncludeSystem $(SRC_DIR)
```

* Kutilgan xatoliklar, noto‘g‘ri foydalanishlar uchun kodni tekshiradi.

```make
cppcheck_report:
    cppcheck ... --checkers-report=report.txt ... 2> cppcheck_output.log
```

* Natijalarni faylga yozadi: `report.txt` va `cppcheck_output.log`.

```make
read_report:
    ... cat cppcheck_output.log ...
```

* Log fayllarni terminalga chiqaradi.

```make
clear_log:
    find $(SRC_DIR) ... -name 'cppcheck_output.log' -delete
```

* Log fayllarni o‘chiradi.

---

## 🎨 Kod formatlash:

```make
clang-format:
    clang-format -n $(SRC_DIR)/*.c $(SRC_DIR)/*.h
```

* `*.c` va `*.h` fayllarni `clang-format` bilan tekshiradi (`-n` → faqat tekshiradi, o‘zgartirmaydi).

---

## 🧠 Xotira xatoliklarini tekshirish:

```make
valgrind:
    valgrind --leak-check=full $(Q)
```

* `valgrind` yordamida dasturni ishga tushirib, xotira oqishlari (leaks) ni aniqlaydi.

---

## ▶️ Dastur ishga tushirish:

```make
run:
    [ -f $(Q) ] && $(Q) || echo ...
```

* Agar dastur mavjud bo‘lsa (`../build/graph`) → ishga tushadi.

---

## ℹ️ Yordam (help):

```make
help:
    @echo "Quyidagi buyruqlar mavjud: ..."
```

* Mavjud `make` buyruqlar ro‘yxatini va izohlarini chiqaradi.

---

## 📛 `.PHONY`:

```make
.PHONY: all clean_outs rebuild clean clang-format cppcheck cppcheck_report clear_log run valgrind help
```

* Bu qator `make` ga ushbu maqsadlar (targets) haqiqiy fayl emasligini bildiradi.

---

## Dasturni ishga tushirish:
```bash
make all
make run
```

2. Misol ifoda kiritish:
```
sin(x)*x
```

3. Natija - konsolda grafik ko'rinishda chiqadi.

## Xotira Boshqaruvi

Dasturda dinamik xotira boshqaruvi to'g'ri amalga oshirilgan. Har bir malloc() uchun mos free() chaqiriladi.

## Yaxshilanish Mumkin Bo'lgan Joylar

1. Xatolarni boshqarishni yaxshilash
2. Qo'shimcha matematik funksiyalarni qo'shish
3. Grafik chiqishni rangli qilish
4. Foydalanuvchi interfeysini yaxshilash

Ushbu dastur matematik ifodalarni tahlil qilish, ularni RPN shakliga o'tkazish va grafik ko'rinishda chiqarishning yaxshi namunasidir. C dasturlash tilida yozilganligi sababli, u samaradorlik va past darajadagi nazoratni namoyish etadi.

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
