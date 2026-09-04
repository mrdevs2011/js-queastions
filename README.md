# Quest Questions

Ulugbek Samigjonov **JavaScript** kurslari uchun ochiq savollar banki.

Kimdir o‘z saytiga yoki ilovasiga **CDN orqali** ulab, savollarni olib ishlatishi mumkin.

---

## Kurslar

| ID | Nom | Darslar | Savollar |
|----|-----|---------|----------|
| `js-asoslari` | Javascript asoslari | 30 | ~146 |
| `javascript` | Javascript | 29 | ~140 |

**Jami:** 286 ta savol (test + kod yozish)

---

## Tuzilma

```
quest-questions/
├── manifest.json                 ← barcha kurslar katalogi
└── courses/
    ├── js-asoslari/
    │   ├── lessons.json          ← dars nomlari
    │   ├── index.json            ← packlar ro‘yxati
    │   └── packs/
    │       ├── mcq/
    │       │   ├── lesson-01.json
    │       │   ├── lesson-02.json
    │       │   └── ...
    │       └── code/
    │           ├── lesson-04.json
    │           └── ...
    └── javascript/
        ├── lessons.json
        ├── index.json
        └── packs/
            ├── mcq/
            └── code/
```

---

## Qanday ulash (2 daqiqa)

### 1. Base URL

GitHub repongizga joylagach:

```text
https://cdn.jsdelivr.net/gh/USER/quest-questions@main/
```

`USER` o‘rniga GitHub username yozing.

### 2. Kerakli faylni olish

```js
const BASE = "https://cdn.jsdelivr.net/gh/USER/quest-questions@main/";

// Katalog
const manifest = await fetch(BASE + "manifest.json").then(r => r.json());

// Bitta kurs dars nomlari
const lessons = await fetch(BASE + "courses/js-asoslari/lessons.json").then(r => r.json());

// Bitta dars test savollari
const mcq = await fetch(BASE + "courses/js-asoslari/packs/mcq/lesson-18.json").then(r => r.json());

// Bitta dars kod savollari
const code = await fetch(BASE + "courses/js-asoslari/packs/code/lesson-18.json").then(r => r.json());
```

### 3. Client o‘zi tanlaydi

```js
const config = {
  course: "js-asoslari",   // yoki "javascript"
  types: ["mcq", "code"],  // qaysi turlar
  lessons: [1, 2, 3, 18],  // qaysi darslar (yoki "all")
};
```

Keyin faqat shu dars/pack fayllarini yuklaysiz.

---

## Savol formatlari

### Test (mcq)

```json
{
  "lesson": 18,
  "type": "mcq",
  "title": "if/else",
  "questions": [
    {
      "id": "mcq-18-001",
      "q": "Savol matni?",
      "opts": ["A", "B", "C", "D"],
      "correct": 1,
      "exp": "Qisqa tushuntirish"
    }
  ]
}
```

`correct` — to‘g‘ri javob indeksi (0 dan boshlanadi).

### Kod yozish (code)

```json
{
  "lesson": 18,
  "type": "code",
  "title": "if/else",
  "questions": [
    {
      "id": "code-18-001",
      "task": "Vazifa matni...",
      "sample": "let x = 1;\nconsole.log(x);",
      "exp": "Qisqa tushuntirish"
    }
  ]
}
```

---

## Tezkor yo‘l (barcha packlar ro‘yxati)

```js
const index = await fetch(BASE + "courses/js-asoslari/index.json").then(r => r.json());
// index.mcq  → [{ lesson, file, count }, ...]
// index.code → [{ lesson, file, count }, ...]
```

---

## Qo‘shish / o‘zgartirish

1. Tegishli `lesson-XX.json` ni tahrirlang
2. `index.json` dagi `count` ni yangilang (ixtiyoriy)
3. Push qiling — CDN bir necha daqiqada yangilanadi

Yangi dars qo‘shish: yangi `lesson-XX.json` yarating, `lessons.json` ga nom qo‘shing.

---

## Litsenziya

Ochiq foydalanish uchun. Kurs muallifi: **Ulugbek Samigjonov**.
