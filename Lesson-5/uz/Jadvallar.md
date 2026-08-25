## Jadvallar

> **Oldingi dars bilan bog'lanish:** o'tgan darsda biz rasmlar va mediani joylashtirishni o'rgandik. Bugun ma'lumotlarni ko'rsatishning yana bir usulini ko'rib chiqamiz — jadvallar, qatorlar va ustunlarga mantiqiy tizimlangan ma'lumotlar uchun.

---

## Dars oxiriga qadar nimani o'rganasiz

- `table`, `tr`, `td`, `th` teglari bilan jadvallar qurish.
- `thead`, `tbody`, `tfoot` orqali jadvalni tuzilishga ajratish.
- `colspan` va `rowspan` orqali katakchalarni gorizontal va vertikal yo'nalishda birlashtirish.
- `scope` va `caption` yordamida jadvallarni ekran o'quvchilari uchun qulay qilish.
- Qachon jadvallar mos kelishi va qachon kelmasligini tushunish.

---

## Dars davomiyligi

| Blok                                              | Mazmuni                                   |
| ------------------------------------------------- | ----------------------------------------- |
| 1. Nima uchun jadvallar kerak va qachon ishlatmaslik kerak | Jadval ma'lumotlari vs sahifa tartibga solish |
| 2. table, tr, td, th                              | Jadvalning asosiy tuzilishi               |
| 3. thead, tbody, tfoot                            | Jadvalning mazmuniy ajratilishi           |
| 4. Kichik topshiriq                               | Oddiy jadval yig'ish                      |
| 5. colspan va rowspan                              | Katakchalarni birlashtirish               |
| 6. Jadvallarning qulayligi: caption, scope         | Jadval yorlig'i va sarlavhalar ma'lumotlar bog'lanishi |
| 7. Xulosalar va amaliy topshiriq                   | Mustahkamlash                             |

---

## Blok 1. Nima uchun jadvallar kerak va qachon ishlatmaslik kerak

**Oddiy qilib aytganda:** HTML dagi jadval — bu Excel yoki Word dagi jadval bilan bir xil narsa: qatorlar (gorizontal qatorlar) va ustunlar (vertikal ustunlar) bo'yicha tizimlangan ma'lumotlar, har bir katakchasi ma'lum qator va ma'lum ustun kesishgan joyda joylashgan.

**Jadvallarni qo'llash qoidasi juda oddiy:** `<table>` ni faqat sizda **haqiqatan jadval ma'lumotlari** bo'lganda ishlating — ya'ni qator ham, ustun ham bir vaqtda muhim bo'lgan ma'lumotlar. Yaxshi holatlar misollari:

- dars jadvali (haftaning kuni × vaqt);
- tariflar narxlarini taqqoslash (tarif × xususiyat);
- turnir jadvali (jamoa × ochko/g'alaba/mag'lubiyat);
- o'quvchilar ro'yxati baholar bilan fanlar bo'yicha.

### Muhim tarixiy ogohlantirish

Ko'p yillar oldin (1990-yillarda — 2000-yillarning boshida) veb-dasturchilar jadvallarni **butun sahifaning tartibini qurish uchun** ishlatishardi — ya'ni, sarlavha, menyu va kontentni ekranning to'g'ri joylariga joylashtirish uchun, jadval ma'lumotlari bilan umuman bog'liq emas. Buni **"table layout"** deb atashardi va bugun bu **eski deb hisoblanadi va tavsiya etilmaydi**, chunki:

- bunday kodni o'qish va qo'llab-quvvatlash qiyin;
- ekran o'quvchisi `<table>` ni uchratganda, aynan sarlavhali qator/ustun ma'lumotlarini eshitishni kutadi — bu ko'zi ojiz foydalanuvchilarni adashtiradi;
- zamonaviy CSS (kursda keyinchalik o'rganamiz) sahifada bloklarni joylashtirish uchun ancha moslashuvchan vositalarni beradi.

**Qoida oddiy:** agar siz shunchaki "bloklarni yonma-yon joylashtirmoqchi bo'lsangiz" (masalan, sarlavha tepada, menyu chapda, kontent o'ngda) — bu CSS vazifasi, `<table>` emas. Jadval faqat haqiqiy jadval **ma'lumotlari** uchun.

---

## Blok 2. `table`, `tr`, `td`, `th`

### Asosiy tuzilish

```html
<table>
    <tr>
        <th>Ism</th>
        <th>Yosh</th>
        <th>Shahar</th>
    </tr>
    <tr>
        <td>Aziz</td>
        <td>21</td>
        <td>Toshkent</td>
    </tr>
    <tr>
        <td>Dilnoza</td>
        <td>19</td>
        <td>Almalyk</td>
    </tr>
</table>
```

Har bir tegni ko'rib chiqamiz.

### `<table>` — jadvalning o'zi

Butun jadval uchun umumiy o'roq. Qolgan hamma narsa uning ichida joylashgan.

### `<table>` (table row) — jadval qatori

Jadvalning har bir gorizontal qatori — alohida `<table>` tegi. Yuqoridagi misolda uchta qator: bitta ustun sarlavhalari uchun va ikkitasi ma'lumotlar uchun.

### `<th>` (table header) — sarlavha katakchasi

Qator yoki ustun uchun **sarlavha** ekanini bildiruvchi katakcha, oddiy ma'lumot emas. Brauzer standart holatda uni qalin shrift va markazda ko'rsatadi — lekin, biz 2-darsdan bilganimizdek, muhim ko'rinish emas, ma'no: `<th>` brauzer va ekran o'quvchisiga "bu sarlavha, bu ustun/qatordagi qolgan katakchalar aynan unga tegishli" deb xabar beradi.

### `<td>` (table data) — oddiy ma'lumot katakchasi

Jadvalning qolgan barcha katakchalari, o'z ma'lumotlarini (sarlavhalarni emas) saqlaydigan.

**O'xshatish:** sinf jurnalini tasavvur qiling. Fan nomlari yozilgan yuqori qator ("Matematika", "Fizika", "Tarix") — bu `<th>`, katakchalardagi baholar esa — `<td>`. Birinchi ustundagi o'quvchilar nomlari ham `<th>` (qator sarlavhalari), qolgan barchasi esa `<td>`.

### `<th>` faqat tepada emas — chapda ham bo'lishi mumkin

```html
<table>
    <tr>
        <th></th>
        <th>Matematika</th>
        <th>Fizika</th>
    </tr>
    <tr>
        <th>Aziz</th>
        <td>5</td>
        <td>4</td>
    </tr>
    <tr>
        <th>Dilnoza</th>
        <td>4</td>
        <td>5</td>
    </tr>
</table>
```

Bu yerda sarlavhalar ham tepada (fan nomlari), ham chapda (o'quvchilar ismlari) mavjud — chap yuqchi burchakdagi bo'sh `<th></th>` jadval to'g'ri tekislanishi uchun kerak ("ikki tomonlama" sarlavhali jadvallar uchun bu standart amaliyot).

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xatolik                                                                     | Qanday tuzatish                                                                                                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sarlavhalar uchun `<th>` o'rniga `<td>` ishlatish                            | Qator/ustun sarlavhalari — har doim `<th>`, boshqa tegrar orqali qalin qilinadigan `<td>` emas                                                                   |
| `<tr>`, `<td>`, `<th>` ni yopishni unutish                                  | Uchta teg ham juft, yopuvchi teglarni unutmang                                                                                                                  |
| Sababsiz turli qatorlarda turlicha katakchalar soni bo'lishi                | Har bir `<tr>` bir xil miqdordagi katakchalar (`<td>`/`<th>`)ni o'z ichishi kerak, faqat `colspan`/`rowspan` (5-blok) orqali ongli birlashtirmasangiz         |
| Sahifa bloklarini joylashtirish uchun `<table>` ishlatish (sarlavha/menyu/kontent) | Sahifa tartibga solish uchun CSS ishlating — jadval faqat jadval ma'lumotlari uchun                                                                            |

---

## Blok 3. `thead`, `tbody`, `tfoot`

Jadval kattalashib murakkablashganda, uni mazmuniy qismlarga ajratish foydali — hisobotdagi kabi "jadval sarlavhasi", "asosiy ma'lumotlar" va "yakuniy qator".

```html
<table>
    <thead>
        <tr>
            <th>Mahsulot</th>
            <th>Narx</th>
            <th>Soni</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Noutbuk</td>
            <td>8 000 000 so'm</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Sichqoncha</td>
            <td>150 000 so'm</td>
            <td>2</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Jami</td>
            <td>8 300 000 so'm</td>
            <td>3</td>
        </tr>
    </tfoot>
</table>
```

- **`<thead>`** (table head) — jadval sarlavhasi, odatda ustun sarlavhalari bilan qator(lar).
- **`<tbody>`** (table body) — jadvalning asosiy "tanası", ma'lumotlar joylashgan joy. Jadval uzun bo'lsa (ko'p qatorlar), brauzerda aylantirganda `<thead>` ba'zan tepada mahkamlanishi mumkin, `<tbody>` aylanadi — bu CSS orqali sozlanadi, lekin semantik ajratish bunday xulqning asosidir.
- **`<tfoot>`** (table foot) — jadval pastki qismi, odatda yakunlar uchun (jami, o'rtacha qiymat).

**Muhim:** bu majburiy teglar emas (2-blokdagi oddiy jadval bundan ham to'liq to'g'ri), lekin haqiqiy ma'lumotlar bilan jadvallar uchun — brauzer va ekran o'quvchisiga jadval tuzilishini aniq bildiruvchi yaxshi amaliyot.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xatolik                                                                         | Qanday tuzatish                                                                                                                                                                                             |
| ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ustun sarlavhalarini `<thead>` o'rniga `<tbody>` ichiga joylashtirish            | Sarlavha qator(lar) — `<thead>` ichiga, ma'lumotlar — `<tbody>` ichiga                                                                                                                                      |
| `<tfoot>` ni `<tbody>` dan keyin yozish, uni pastda ko'rsatilishini kutish      | Spetsifikasyonga ko'ra `<tfoot>` koddan oldin ham, keyin ham yozilishi mumkin — brauzer uni vizual jihatdan jadval pastida ko'rsatadi, lekin kodning o'qilishi uchun `thead → tbody → tfoot` tartibida yozish qabul qilinggan |

---

## Kichik topshiriq

Namunalarga qaramasdan, 2 kunlik dars jadvalining oddiy jadvalini mustaqil ravishda yig'ing: "Kun" va "Fan" ustunlari, `<thead>` va `<tbody>` ishlatgan holda.

**Yechim:**

```html
<table>
    <thead>
        <tr>
            <th>Kun</th>
            <th>Fan</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Dushanba</td>
            <td>Matematika</td>
        </tr>
        <tr>
            <td>Seshanba</td>
            <td>Fizika</td>
        </tr>
    </tbody>
</table>
```

---

## Blok 5. `colspan` va rowspan` — katakchalarni birlashtirish

Ba'zan bitta katakcha bir nechta ustun yoki qator bo'ylab "cho'zilishi" kerak — masalan, ikki ustunga tegishli sarlavha.

### `colspan` — gorizontal birlashtirish (ustunlar)

```html
<table>
    <tr>
        <th colspan="2">Aloqa ma'lumotlari</th>
    </tr>
    <tr>
        <td>Email</td>
        <td>info@saydullayev.fun</td>
    </tr>
    <tr>
        <td>Telefon</td>
        <td>+998 90 123-45-67</td>
    </tr>
</table>
```

`colspan="2"` — "bu katakcha kenglikda ikki oddiy katakchaning o'rnini egallaydi" degani — shuning uchun birinchi qatorda faqat bitta `<th>`, lekin u vizual jihatdan jadvalning to'liq kengligiga cho'ziladi (2 katakcha o'rnini egallaydi).

**O'xshatish:** katakchali varaqda ikki qo'shni katakcha orasidagini chegarani o'chirib, hosil bo'lgan birlashgan maydonda bitta matn yozing — aynan shu narsani `colspan` qiladi.

### `rowspan` — vertikal birlashtirish (qatorlar)

```html
<table>
    <tr>
        <th>Ism</th>
        <th>Fan</th>
        <th>Baho</th>
    </tr>
    <tr>
        <td rowspan="2">Aziz</td>
        <td>Matematika</td>
        <td>5</td>
    </tr>
    <tr>
        <td>Fizika</td>
        <td>4</td>
    </tr>
</table>
```

`rowspan="2"` — "bu katakcha balandlikda ikki qatorning o'rnini egallaydi" degani — shuning uchun "Aziz" nomi ikki marta takrorlanmaydi, ikkala bahosiga ham bir marta ko'rsatiladi.

**`colspan`/`rowspan` ishlatishda muhim qoida:** siz katakchani bir nechta ustun/qatorga birlashtirsangiz, shu qator/ustunda oddiy katakchalar **kamroq** bo'lishi kerak — birlashtirilgan katakcha "yegan" miqdordagicha kamroq. `rowspan="2"` misolida ikkinchi `<tr>` qatori faqat 2 katakchadan iborat (`<td>Fizika</td><td>4</td>`), 3 ta emas — chunki birinchi katakchaning o'rnini allaqachon birinchi qatardagi birlashtirilgan katakcha "egallagan".

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xatolik                                                                  | Qanday tuzatish                                                                                                                                                                |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Birlashtirishdan keyin qator/ustundagi katakchalar sonini kamaytirishni unutish | Agar bir qatorda `rowspan="2"` ishlatilgan bo'lsa — keyingi qatorda bitta katakcha kamroq bo'lishi kerak                                                                          |
| `colspan` (gorizontal, ustunlar) va `rowspan` (vertikal, qatorlarni) adashtirish | Eslab qoling: col = column = ustun → `colspan` ustunlar bo'ylab cho'zadi (kenglikka); row = qator → `rowspan` qatorlar bo'ylab cho'zadi (balandlikka)                            |
| Murakkab jadvallarda katakchalarni haddan tashqari birlashtirish         | `colspan`/`rowspan` ni faqat ma'lumotlarni tushunishni haqiqatan osonlashtirgandagina ishlating — ortiqcha birlashtirish kodni va jadvalni qiyinlashtiradi, ayniqsa ekran o'quvchilari uchun |

---

## Blok 6. Jadvallarning qulayligi: `caption` va `scope`

### `<caption>` — jadval yorligi/nomi

```html
<table>
    <caption>Haftalik dars jadvali</caption>
    <thead>
        <tr>
            <th>Kun</th>
            <th>Fan</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Dushanba</td>
            <td>Matematika</td>
        </tr>
    </tbody>
</table>
```

`<caption>` — `<table>` ichidagi birinchi ichki element (ochuvchi `<table>` tegidan darhol keyin, `<thead>` dan oldin). U jadvalga nom beradi — bosma hujjatdagi "1-jadval. Dars jadvali" sarlavhasiga o'xshaydi. Ekran o'quvchisi jadval tarkibini o'qishdan oldin `<caption>` ni ovozli o'qiydi — bu foydalanuvchiga darhol jadval nima haqida ekanini tushunishga yordam beradi.

### `scope` — sarlavha va ma'lumotlar bog'lanishi

`<th>` tegidagi `scope` atributi bu sarlavha nisbatan nimaga ekanini — ustunga yoki qatorga — aniq ko'rsatadi. Bu ekran o'quvchilari uchun juda muhim: foydalanuvchi ma'lumotlar katakchalari bo'ylab harakatlanayotganda, ekran o'quvchisi tegishli sarlavhani avtomatik ovozli aytib berishi mumkin, foydalanuvchiga kontekstni "eslatadi" (masalan: "5, Matematika bahosi, Azizda" — oddiy "5" o'rniga).

```html
<table>
    <caption>O'quvchilar baholari</caption>
    <thead>
        <tr>
            <th scope="col">Ism</th>
            <th scope="col">Matematika</th>
            <th scope="col">Fizika</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Aziz</th>
            <td>5</td>
            <td>4</td>
        </tr>
        <tr>
            <th scope="row">Dilnoza</th>
            <td>4</td>
            <td>5</td>
        </tr>
    </tbody>
</table>
```

- `scope="col"` — sarlavha ostidagi butun **ustun** ga tegishli.
- `scope="row"` — sarlavha yonidagi butun **qator** ga tegishli.

**O'xshatish:** telefon orqali jadvalni ko'rmasdan tushuntirayotgandek tasavvur qiling. `scope` sizsiz siz shunchaki raqamlarni ketma-ket aytasiz — ma'nosiz. `scope` bilan siz har safar "bu Azizning Matematika bahosi" deb aniqlaysiz — aynan shunday ekran o'quvchisi ushbu atribut tufayli ishlaydi.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xatolik                                                                                                | Qanday tuzatish                                                                                                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `<caption>` ni tashlab, faqat jadval yonidagi matnga ishonish (masalan, `<table>` dan oldingi `<h2>`)    | Aniq `<caption>` ni `<table>` ichida ishlating — u jadvalga semantik bog'langan, yaqin atrofdagi ixtiyoriy matndan farqli o'laroq      |
| `<th>` da `scope` ko'rsatmaslik                                                                       | `scope="col"` yoki `scope="row"` qo'shing — ayniqsa qator va ustun bo'yicha sarlavhali jadvallar uchun juda muhim                   |
| `<caption>` ni `<table>` ichidagi birinchi element qilmay joylashtirish                                 | `<caption>` ochuvchi `<table>` tegidan darhol keyin, `<thead>` dan oldin kelishi kerak                                                |

---

## Dars xulosalari

Bugun siz o'rgandingiz:

- Jadvallar (`<table>`) **haqiqiy jadval ma'lumotlari** uchun mo'ljallangan, sahifa tartibga solish uchun emas — bu eski va tavsiya etilmaydigan amaliyot.
- `<tr>` — qator, `<th>` — sarlavha katakchasi, `<td>` — ma'lumot katakchasi.
- `<thead>`, `<tbody>`, `<tfoot>` jadvalni mazmuniy jihatdan sarlavha, tana va pastki qismga ajratadi.
- `colspan` katakchalarni gorizontal (ustunlar), `rowspan` — vertikal (qatorlar) yo'nalishda birlashtiradi.
- `<caption>` jadvalga nom beradi, `<th>` dagi `scope="col"`/`scope="row"` esa ekran o'quvchilari uchun sarlavhalarni ma'lumotlar bilan bog'laydi.
