---
title: Conway O'yinini c dasturlash tilida yaratish
description: Ushbu maqolada 21-maktab basseynining "Piscine C" dasturining birinchi bosqichiga tayyorlanish uchun mo‘ljallangan, bajarilgan va izohlangan vazifalarning turli versiyalari taqdim etilgan.
author: yorenwyl
date: 2025-06-15 21:43:00 +0500
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



### Conway O'yini tarixi

Conwayning "Hayot O'yini" (Conway's Game of Life) — bu juda oddiy va eng ko'p ommalashgan hujayrali avtomatlardan biridir. 1970-yilda ingliz matematikasi Jon Xorton Konvay tomonidan yaratilgan bu o'yin, ayniqsa, uning o'ziga xos qoidalari bilan diqqatga sazovor. O'yin maqsadi – tasodifiy tarzda boshlang'ich holat berilgan maydon bo'ylab hayot va o'limni simulyatsiya qilishdir. Bu o'yinda eng muhim jihat shundaki, uning rivojlanishi har qanday tashqi aralashuvsiz faqat dastlabki holatga bog'liq.

### O'yin qoidalari

Conway o'yini juda sodda qoidalarga asoslanadi:

1. **Yashash**: Agar tirik hujayraning atrofida 2 yoki 3 ta tirik qo'shni bo'lsa, u yashaydi.
2. **O'lim**: Agar tirik hujayrada 2 ta qo'shni bo'lsa, u yashaydi; agar 1 ta yoki 0 ta qo'shni bo'lsa, o'ladi (yuqoridan pastga) — bu "kamchilik" (underpopulation).
3. **Tirik hujayra ko'payishi**: Agar o'lik hujayraning atrofida aynan 3 ta tirik qo'shni bo'lsa, u tirik bo'ladi (yangi hayot).

O'yinning rivojlanishi to'liq avtomatik bo'lib, bu o'yinda hech qanday foydalanuvchi aralashuvi bo'lmaydi.

### Kodingizni tushunish

Siz keltirgan kod C dasturlash tilida yozilgan va **ncurses** kutubxonasidan foydalanadi, bu esa terminalda o'yinning vizualizatsiyasini amalga oshirishga yordam beradi. Quyida kodning asosiy qismlarini tahlil qilamiz.

#### 1. **Konstantalar va o'zgaruvchilar**:

```c
#define ROWS 25
#define COLS 80
#define ALIVE 1
#define DEAD 0
```

Bu qismda o'yin maydonining o'lchamlari va hujayraning tirik (`ALIVE`) yoki o'lik (`DEAD`) holatini aniqlash uchun konstantalar belgilanadi. Maydon 25 qator va 80 ustundan iborat.

#### 2. **Maydonni boshlash (init\_grid)**:

```c
void init_grid(int grid[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            grid[i][j] = DEAD;
        }
    }
}
```

`init_grid` funktsiyasi barcha hujayralarni boshlang'ich holatda — o'lik deb o'rnatadi. Bu maydonni tozalashni ta'minlaydi.

#### 3. **Maydonni chiqarish (print\_grid)**:

```c
void print_grid(const int grid[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printw("%c", grid[i][j] ? 'O' : ' ');
        }
        printw("\n");
    }
}
```

`print_grid` funktsiyasi maydonni ekranga chiqarish uchun javobgardir. Tirik hujayralar `'O'` belgisi bilan, o'liklar esa bo'sh joy (`' '`) bilan ko'rsatiladi.

#### 4. **Qo'shnilarni sanash (count\_neighbors)**:

```c
int count_neighbors(const int grid[ROWS][COLS], int x, int y) {
    int count = 0;
    for (int dx = -1; dx <= 1; dx++) {
        for (int dy = -1; dy <= 1; dy++) {
            if (dx == 0 && dy == 0) continue;
            int nx = (x + dx + ROWS) % ROWS;
            int ny = (y + dy + COLS) % COLS;
            count += grid[nx][ny];
        }
    }
    return count;
}
```

`count_neighbors` funktsiyasi berilgan (x, y) koordinatdagi hujayraning atrofidagi tirik hujayralarni sanaydi. Bu funktsiya maydonning chegaralarini hisobga olgan holda ishlaydi, ya'ni chetga chiqqan hujayralar qayta o'zgarib turadi (modulga asoslangan).

#### 5. **Maydonni yangilash (update\_grid)**:

```c
void update_grid(int current[ROWS][COLS], int next[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            int neighbors = count_neighbors(current, i, j);
            next[i][j] = (neighbors == 3 || (current[i][j] && neighbors == 2)) ? ALIVE : DEAD;
        }
    }
}
```

`update_grid` funktsiyasi har bir hujayraning keyingi holatini hisoblab, yangi maydonni (next) yaratadi. Hujayraning tirik yoki o'lik bo'lishi uning qo'shnilari soniga bog'liq.

#### 6. **Glayder (Glider) shaklini o'rnatish**:

```c
void setup_glider(int grid[ROWS][COLS]) {
    grid[1][2] = ALIVE;
    grid[2][3] = ALIVE;
    grid[3][1] = ALIVE;
    grid[3][2] = ALIVE;
    grid[3][3] = ALIVE;
}
```

`setup_glider` funktsiyasi o'yin maydonida "glider" shaklini yaratadi. Glayder — bu o'yin davomida harakatlanadigan va o'zining shaklini saqlaydigan bir nechta tirik hujayralardan iborat maxsus shakldir.

#### 7. **Fayldan boshlang'ich holatni yuklash (load\_from\_file)**:

```c
void load_from_file(int grid[ROWS][COLS], const char *filename) {
    FILE *file = fopen(filename, "r");
    if (!file) {
        printw("File ochib bo'lmadi: %s\n", filename);
        refresh();
        napms(2000);
        setup_glider(grid);
        return;
    }

    char line[COLS + 2];
    int row = 0;

    while (fgets(line, sizeof(line), file) && row < ROWS) {
        int line_len = my_strlen(line);
        for (int col = 0; col < COLS && col < line_len; col++) {
            grid[row][col] = (line[col] == 'O') ? ALIVE : DEAD;
        }
        row++;
    }

    fclose(file);
}
```

`load_from_file` funktsiyasi tashqi fayldan o'yin boshlang'ich holatini yuklab olish imkonini beradi. Agar fayl ochilmasa, "glider" shakli o'rnatiladi.

### Xulosa

Conway o'yini o'zining oddiy va minimalist qoidalari bilan juda murakkab va go'zal simulyatsiyalar yaratadi. Sizning kodingiz esa, bu o'yinni terminalda haqiqiy vaqt rejimida vizual tarzda ko'rsatadi. Har bir qadamingizni batafsil kuzatish, o'yin qanday ishlashini va undagi o'zgarishlarni to'liq tushunish uchun juda foydali. Bu kod C dasturlash tilida yaratilgan bo'lib, ncurses kutubxonasidan foydalangan holda terminalda o'yinni ko'rsatadi.
