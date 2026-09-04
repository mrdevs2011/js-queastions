# js-queastions

Ulugbek Samigjonov **JavaScript** kurslari uchun ochiq savollar banki.

Har kim o‘z sayti yoki ilovasiga **CDN** orqali ulab, kerakli kurs / dars / turdagi savollarni olib ishlatishi mumkin.

**Repo:** [github.com/mrdevs2011/js-queastions](https://github.com/mrdevs2011/js-queastions)

---

## CDN (jsDelivr)

```text
https://cdn.jsdelivr.net/gh/mrdevs2011/js-queastions@main/
```

---

## Kurslar

| ID | Nom | Darslar | Savollar (taxminan) |
|----|-----|---------|---------------------|
| `js-asoslari` | Javascript asoslari | 30 | MCQ + kod |
| `javascript` | Javascript | 29 | MCQ + kod |

**Jami:** 1500+ savol (test + kod yozish)

---

## Tuzilma

```text
js-queastions/
├── README.md
├── manifest.json              ← barcha kurslar katalogi
└── courses/
    ├── js-asoslari/
    │   ├── lessons.json       ← dars nomlari
    │   ├── index.json         ← packlar ro‘yxati + statistika
    │   └── packs/
    │       ├── mcq/
    │       │   ├── lesson-01.json
    │       │   └── ...
    │       └── code/
    │           ├── lesson-01.json
    │           └── ...
    └── javascript/
        ├── lessons.json
        ├── index.json
        └── packs/
            ├── mcq/
            └── code/
```

---

## Qanday ulash

### 1. Base URL

```js
const BASE = "https://cdn.jsdelivr.net/gh/mrdevs2011/js-queastions@main/";
```

### 2. Katalog va darslar

```js
// Barcha kurslar
const manifest = await fetch(BASE + "manifest.json").then(r => r.json());

// Bitta kurs dars nomlari
const lessons = await fetch(BASE + "courses/js-asoslari/lessons.json").then(r => r.json());

// Packlar ro‘yxati (qaysi darsda nechta savol)
const index = await fetch(BASE + "courses/js-asoslari/index.json").then(r => r.json());
```

### 3. Bitta dars savollari

```js
// Test (variantli)
const mcq = await fetch(BASE + "courses/js-asoslari/packs/mcq/lesson-18.json")
  .then(r => r.json());

// Kod yozish
const code = await fetch(BASE + "courses/js-asoslari/packs/code/lesson-18.json")
  .then(r => r.json());
```

### 4. Client o‘zi tanlaydi

```js
const config = {
  course: "js-asoslari",   // yoki "javascript"
  types: ["mcq", "code"],  // qaysi turlar
  lessons: [1, 2, 3, 18],  // qaysi darslar
  // yoki: lessons: "all"
};
```

Keyin faqat kerakli `lesson-XX.json` fayllarini yuklaysiz.

---

## Savol formatlari

### Test (`mcq`)

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

`correct` — to‘g‘ri javob indeksi (**0** dan boshlanadi).

### Kod yozish (`code`)

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

## Tezkor misol: 1–5 dars MCQ yuklash

```js
const BASE = "https://cdn.jsdelivr.net/gh/mrdevs2011/js-queastions@main/";
const course = "js-asoslari";
const lessons = [1, 2, 3, 4, 5];

const packs = await Promise.all(
  lessons.map(n => {
    const id = String(n).padStart(2, "0");
    return fetch(`${BASE}courses/${course}/packs/mcq/lesson-${id}.json`).then(r => r.json());
  })
);

const allQuestions = packs.flatMap(p => p.questions);
console.log(allQuestions.length);
```

---

## Qo‘shish / o‘zgartirish

1. Tegishli `lesson-XX.json` ni tahrirlang  
2. Kerak bo‘lsa `index.json` dagi `count` ni yangilang  
3. `git push` — CDN odatda bir necha daqiqada yangilanadi  

Yangi dars: yangi `lesson-XX.json` + `lessons.json` ga nom qo‘shing.

---

## Litsenziya

Ochiq foydalanish uchun.  
Kurs muallifi: **Ulugbek Samigjonov**.  
Repo: [mrdevs2011/js-queastions](https://github.com/mrdevs2011/js-queastions).
