---
title: Conway O'yinini c dasturlash tilida yaratish
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichiga tayyorlanish uchun mo‘ljallangan, bajarilgan va izohlangan vazifalarning turli versiyalari taqdim etilgan.
author: yorenwyl
date: 2025-06-15 21:43:00 +0500
categories: [21-IT Maktab - School 21, Basseyn - C Piscine]
tags: [Basseyn - C Piscine]
pin: true
image:
  path: /conway.gif
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 21-IT Maktab - School 21.
media_subpath: "/assets/img/articles/2025-03-26-basseynga-tayyorlanish/"
---

---

### Conway O'yini tarixi

Conwayning "Hayot O'yini" (Conway's Game of Life) — bu juda oddiy va eng ko'p ommalashgan hujayrali avtomatlardan biridir. 1970-yilda ingliz matematikasi Jon Xorton Konvay tomonidan yaratilgan bu o'yin, ayniqsa, uning o'ziga xos qoidalari bilan diqqatga sazovor. O'yin maqsadi – tasodifiy tarzda boshlang'ich holat berilgan maydon bo'ylab hayot va o'limni simulyatsiya qilishdir. Bu o'yinda eng muhim jihat shundaki, uning rivojlanishi har qanday tashqi aralashuvsiz faqat dastlabki holatga bog'liq.

### O'yin qoidalari

Conway o'yini juda sodda qoidalarga asoslanadi:

1. **Yashash**: Agar tirik hujayraning atrofida 2 yoki 3 ta tirik qo'shni bo'lsa, u yashaydi.
2. **O'lim**: Agar tirik hujayrada 2 ta qo'shni bo'lsa, u yashaydi; agar 1 ta yoki 0 ta qo'shni bo'lsa, o'ladi (yuqoridan pastga) — bu "kamchilik" (underpopulation).
3. **Tirik hujayra ko'payishi**: Agar o'lik hujayraning atrofida aynan 3 ta tirik qo'shni bo'lsa, u tirik bo'ladi (yangi hayot).

O'yinning rivojlanishi to'liq avtomatik bo'lib, bu o'yinda hech qanday foydalanuvchi aralashuvi bo'lmaydi.

### Kodni tushunish

SKeltirilgan kod C dasturlash tilida yozilgan va **ncurses**, **stdio** kutubxonalaridan foydalanadi, bu esa terminalda o'yinning vizualizatsiyasini amalga oshirishga yordam beradi. Quyida kodning asosiy qismlarini tahlil qilamiz.

```
/*
 *Copyrights 2025 yorenwyl, ismaelja (Leader), onionscy Samarkand
 */

// ncurses kutubxonasi: terminal interfeysini boshqarish uchun kerak
#include <ncurses.h>

// stdio.h: fayl o‘qish va chiqarish funksiyalari uchun kerak
#include <stdio.h>

// O‘yin maydonining o‘lchamlari
#define ROWS 25     // Maydonning satrlar soni
#define COLS 80     // Maydonning ustunlar soni

// Huja holatlari
#define ALIVE 1     // Huja tirik bo‘lsa
#define DEAD 0      // Huja o‘lik bo‘lsa

// stdio.h kutubxonasiga tegishli, satr uzunligini hisoblaydi
int my_strlen(const char *str) {
    int len = 0;
    while (str[len] != '\0') len++;  // '\0' belgigacha sanaydi
    return len;
}

// Maydonni boshlang‘ich o‘lik holatga to‘ldiradi
void init_grid(int grid[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {              // Har bir satr uchun
        for (int j = 0; j < COLS; j++) {          // Har bir ustun uchun
            grid[i][j] = DEAD;                   // Huja o‘lik holatga o‘rnatiladi
        }
    }
}

// ncurses.h: Maydonni terminalga chiqarish funksiyasi
void print_grid(const int grid[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {              // Har bir satr uchun
        for (int j = 0; j < COLS; j++) {          // Har bir ustun uchun
            printw("%c", grid[i][j] ? 'O' : ' '); // Tiriksini 'O', o‘likni bo‘sh joy sifatida chiqaradi
        }
        printw("\n");                            // Yangi qator
    }
}

// Qo‘shni hujayralar sonini hisoblaydi (8 atrofdagi hujayra)
int count_neighbors(const int grid[ROWS][COLS], int x, int y) {
    int count = 0;
    for (int dx = -1; dx <= 1; dx++) {             // x yo‘nalishda -1, 0, 1 bo‘ylab yuradi
        for (int dy = -1; dy <= 1; dy++) {         // y yo‘nalishda -1, 0, 1 bo‘ylab yuradi
            if (dx == 0 && dy == 0) continue;      // O‘zini hisobga olmaydi
            int nx = (x + dx + ROWS) % ROWS;       // Yangi x koordinata (chegaradan o‘tishda aylanish)
            int ny = (y + dy + COLS) % COLS;       // Yangi y koordinata (chegaradan o‘tishda aylanish)
            count += grid[nx][ny];                 // Tiriksini 1 qo‘shadi, o‘lik bo‘lsa 0
        }
    }
    return count;  // Qo‘shni tirik hujayralar soni
}

// current dan kelajakdagi next holatga o‘tadi
void update_grid(int current[ROWS][COLS], int next[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {                             // Har bir satr uchun
        for (int j = 0; j < COLS; j++) {                         // Har bir ustun uchun
            int neighbors = count_neighbors(current, i, j);     // Qo‘shnilar sonini hisoblaydi
            next[i][j] = (neighbors == 3 ||                     // 3 qo‘shni bo‘lsa, tiriladi
                          (current[i][j] && neighbors == 2))    // 2 qo‘shni bo‘lsa, tirik qoladi
                         ? ALIVE : DEAD;                        // Aks holda o‘ladi
        }
    }
}

// Glider (harakatlanuvchi shakl) ni joylashtiradi
void setup_glider(int grid[ROWS][COLS]) {
    grid[1][2] = ALIVE;
    grid[2][3] = ALIVE;
    grid[3][1] = ALIVE;
    grid[3][2] = ALIVE;
    grid[3][3] = ALIVE;
}

// Fayldan boshlang‘ich holatni yuklash (stdio.h)
void load_from_file(int grid[ROWS][COLS], const char *filename) {
    FILE *file = fopen(filename, "r");                 // Faylni ochish (o‘qish rejimida)
    if (!file) {                                       // Fayl ochilmasa
        printw("File ochib bo'lmadi: %s\n", filename); // Xatolik xabari
        refresh();                                     // ncurses oynani yangilash
        napms(2000);                                   // 2 soniya kutish
        setup_glider(grid);                            // Standart glider o‘rnatish
        return;
    }

    char line[COLS + 2];   // Har bir qatorni saqlash uchun
    int row = 0;

    while (fgets(line, sizeof(line), file) && row < ROWS) {    // Har bir qatorda
        int line_len = my_strlen(line);                        // Qator uzunligini topish
        for (int col = 0; col < COLS && col < line_len; col++) {  // Har bir belgini o‘qish
            grid[row][col] = (line[col] == 'O') ? ALIVE : DEAD;   // 'O' - tirik, boshqasi - o‘lik
        }
        row++; // Keyingi qatorga o‘tish
    }

    fclose(file);  // Faylni yopish
}

int main(int argc, char *argv[]) {
    int current[ROWS][COLS], next[ROWS][COLS];  // Maydon holatlari
    int speed = 400;                             // Animatsiya tezligi (millisekund)
    int ch;                                      // Klaviatura kirish belgisi

    initscr();                  // ncurses: terminal oynasini boshlash
    cbreak();                   // ncurses: real vaqtli kirish
    noecho();                   // ncurses: tugmalar bosilishini ko‘rsatmaslik
    nodelay(stdscr, TRUE);      // ncurses: kutmasdan getch() ishlaydi
    curs_set(0);                // ncurses: kursorni yashirish
    init_grid(current);         // Bosh maydonni o‘chirish (hamma hujayra o‘lik)

    if (argc > 1) {                       // Agar fayl nomi berilgan bo‘lsa
        load_from_file(current, argv[1]); // Fayldan holatni o‘qish
    } else {
        setup_glider(current);           // Aks holda gliderni o‘rnatish
    }

    while (1) {                          // Asosiy o‘yin tsikli (doimiy)
        clear();                         // ncurses: ekran tozalash
        print_grid(current);            // Maydonni chizish
        printw("Tezlik: %dms (A - tezroq, Z - sekinroq, SPACE - chiqish)", speed); // Foydalanuvchi uchun ma'lumot
        refresh();                       // ncurses: yangilash

        if ((ch = getch()) != ERR) {     // Agar tugma bosilgan bo‘lsa
            if (ch == ' ') break;        // SPACE bosilsa chiqish
            if (ch == 'a' && speed > 50) speed -= 50;   // A bosilsa - tezlashtirish
            if (ch == 'z' && speed < 1000) speed += 50; // Z bosilsa - sekinlashtirish
        }

        update_grid(current, next);      // Keyingi holatni hisoblash

        for (int i = 0; i < ROWS; i++) {             // Har bir satr
            for (int j = 0; j < COLS; j++) {         // Har bir ustun
                current[i][j] = next[i][j];          // Kelajak holatni hozirgi holatga nusxalash
            }
        }

        napms(speed);                   // Kutish (ncurses): tezlikka qarab
    }

    endwin();                           // ncurses: terminalni qayta tiklash
    return 0;                           // Dasturni muvaffaqiyatli yakunlash
}
```

`load_from_file` funktsiyasi tashqi fayldan o'yin boshlang'ich holatini yuklab olish imkonini beradi. Agar fayl ochilmasa, "glider" shakli o'rnatiladi.

Albatta! Quyida sizning **Conway’s Game of Life** C dasturingizni qanday **kompilyatsiya qilish**, **ishga tushurish** va qanday **parametrlar bilan ishlash** haqida to‘liq yo‘riqnoma yozdim.

---

## 🚀 Dastur Ishga Tushirish Yo‘riqnomasi

### 1. ✅ **Kerakli kutubxonalar**

Ushbu kod quyidagi **kutubxonalarga tayanadi**:

* `ncurses.h` – terminalda grafik ko‘rinishni chizish uchun (`printw`, `refresh`, `napms`, `initscr`, `getch`, va h.k.).
* `stdio.h` – fayllar bilan ishlash va oddiy kirish-chiqish (`fopen`, `fgets`, `printf`, va h.k.).

---

### 2. 🛠 **Kompilyatsiya qilish**

C faylni kompilyatsiya qilish uchun terminalda quyidagi buyruqni yozing (misol uchun fayl nomi `game_of_life.c` bo‘lsa):

```bash
gcc game_of_life.c -o game_of_life -lncurses
```

> Bu yerda:
>
> * `gcc` – GNU Compiler.
> * `-o game_of_life` – chiqadigan fayl nomi.
> * `-lncurses` – `ncurses` kutubxonasini ulaydi.

---

### 3. ▶️ **Ishga tushirish**

#### ✅ 3.1. **Oddiy ishga tushirish (glider bilan)**

Agar siz hech qanday fayl bermasangiz, dastur standart `glider` pattern bilan boshlanadi:

```bash
./game_of_life
```

#### ✅ 3.2. **Fayldan o‘qish bilan ishga tushirish**

Agar siz faylga yozilgan boshlang‘ich holatni yuklamoqchi bo‘lsangiz:

```bash
./game_of_life patterns/glider.txt
```

> `patterns/glider.txt` – bu faylda har bir qator `O` va bo‘sh joylardan iborat bo‘lishi kerak.
> Masalan:
>
> ```
>  O 
>   O
> OOO
> ```

---

### 4. ⌨️ **Interaktiv boshqaruv**

Ishlash vaqtida siz quyidagi tugmalar orqali o‘yinni boshqarishingiz mumkin:

| Tugma   | Vazifasi                             |
| ------- | ------------------------------------ |
| `A`     | Tezlikni **oshiradi** (ya’ni tezroq) |
| `Z`     | Tezlikni **kamaytiradi** (sekinroq)  |
| `SPACE` | O‘yinni to‘xtatadi va chiqadi        |

---

### 5. 📁 Misol patternlar (matnli fayl ko‘rinishida)

Siz quyidagi faylni yaratishingiz mumkin (`glider.txt`):

```text
  O 
   O
 OOO
```

Yuqoridagi faylni `patterns/` papkasida saqlang, keyin:

```bash
./game_of_life patterns/glider.txt
```

---

### 6. 📌 Tavsiyalar

* Terminal hajmini **kamida 80x25** qilganingizga ishonch hosil qiling.
* Har xil `pattern` fayllarni sinab ko‘ring: `block.txt`, `blinker.txt`, `beacon.txt` va h.k.
* Kodni modul qilish uchun `header.h`, `utils.c`, `patterns.c` kabi fayllarga bo‘lish mumkin.

---

## 🧬 1. **Patternlar turlari**

**Conway's Game of Life** loyihangizdagi **`pattern` (shakllar, andozalar)** haqida tushuncha beraman. Bu shakllar o'yin maydonida qanday ko'rinishga ega bo'lishi, qanday harakat qilishi, va ularni qanday yaratish haqida **izohlar bilan** tushuntirib beraman. Keyin siz bularni kodingizga qo‘shishingiz yoki fayldan yuklashingiz mumkin.

---

### 🔹 1. **Glider (Slayder / Sirpanuvchi)**

* **Xususiyatlari**: Har bosqichda chap-ustdan o‘ng-pastga harakatlanadi.
* **Stabil emas, lekin o‘zini ko‘chiradi (self-replicating motion).**
* **Kichik va mashhur pattern.**

```
. O .
. . O
O O O
```

**Ko‘rinish (matnli faylda):**

```
 O 
  O
OOO
```

**Kodga qo‘shilishi:**

```c
void setup_glider(int grid[ROWS][COLS]) {
    grid[1][2] = ALIVE;
    grid[2][3] = ALIVE;
    grid[3][1] = ALIVE;
    grid[3][2] = ALIVE;
    grid[3][3] = ALIVE;
}
```

---

### 🔹 2. **Block (Statik - harakatsiz)**

* **Xususiyatlari**: O‘zgarmaydi, stabil pattern.
* **Foydali sinov uchun.**

```
O O
O O
```

**Ko‘rinish (matnda):**

```
OO
OO
```

**Qo‘shish:**

```c
void setup_block(int grid[ROWS][COLS]) {
    grid[10][10] = ALIVE;
    grid[10][11] = ALIVE;
    grid[11][10] = ALIVE;
    grid[11][11] = ALIVE;
}
```

---

### 🔹 3. **Blinker (O‘zgaruvchan - osillator)**

* **Xususiyatlari**: Har 2 yurishda shakli o‘zgaradi.
* **Oddiy osillator.**

```
Step 1:     Step 2:
 O          O O O
 O   -->     
 O          
```

**Ko‘rinish (faylda):**

```
O
O
O
```

**Qo‘shish:**

```c
void setup_blinker(int grid[ROWS][COLS]) {
    grid[12][15] = ALIVE;
    grid[13][15] = ALIVE;
    grid[14][15] = ALIVE;
}
```

---

### 🔹 4. **Toad (2-bosqichli osillator)**

* **Xususiyatlari**: Har 2 yurishda o‘zgaradi.
* **Kattaroq va murakkab osillator.**

```
Bosqich 1:      Bosqich 2:
 . O O O          O . .
O O O .           . O O
```

**Qo‘shish:**

```c
void setup_toad(int grid[ROWS][COLS]) {
    grid[10][11] = ALIVE;
    grid[10][12] = ALIVE;
    grid[10][13] = ALIVE;
    grid[11][10] = ALIVE;
    grid[11][11] = ALIVE;
    grid[11][12] = ALIVE;
}
```

---

### 🔹 5. **Beacon (To‘rt bosqichli osillator)**

* **Xususiyatlari**: To‘rt yurishda bir holatga qaytadi.
* **2ta blokdan tashkil topgan murakkab osillator.**

```
Bosqich 1:
OO..
OO..
..OO
..OO
```

**Qo‘shish:**

```c
void setup_beacon(int grid[ROWS][COLS]) {
    grid[5][5] = ALIVE;
    grid[5][6] = ALIVE;
    grid[6][5] = ALIVE;
    grid[6][6] = ALIVE;
    grid[7][7] = ALIVE;
    grid[7][8] = ALIVE;
    grid[8][7] = ALIVE;
    grid[8][8] = ALIVE;
}
```

---

### 🔹 Fayldan yuklash uchun misol (`patterns/glider.txt`):

```
  O 
   O
 OOO
```

Buni yuklash uchun siz ilgari keltirgan `load_from_file()` funksiyasidan foydalaniladi.

---
### Xulosa

Conway o'yini o'zining oddiy va minimalist qoidalari bilan juda murakkab va go'zal simulyatsiyalar yaratadi. Sizning kodingiz esa, bu o'yinni terminalda haqiqiy vaqt rejimida vizual tarzda ko'rsatadi. Har bir qadamingizni batafsil kuzatish, o'yin qanday ishlashini va undagi o'zgarishlarni to'liq tushunish uchun juda foydali. Bu kod C dasturlash tilida yaratilgan bo'lib, ncurses kutubxonasidan foydalangan holda terminalda o'yinni ko'rsatadi.
