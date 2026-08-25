## Formatlar qism-2

> **Oldingi dars bilan bog'lanish:** o'tgan darsda biz asosiy forma maydonlarini (text, email, password, number, date, checkbox, radio) va `label`/`for`/`id` bog'lanishini o'rgandik. Bugun qolgan forma elementlarini tugallab, maydonlarni guruhlash va JavaScript ishlatmasdan kiritishni tekshirishni o'rganamiz.

---

## Dars oxiriga qadar nimalarni o'rganasiz

- `select`/`option` orqali ochiladigan ro'yxatlar yaratish, `optgroup` orqali variantlarni guruhlash.
- Ko'p qatorli matn uchun `textarea` ishlatish.
- `fieldset`/`legend` orqali bog'liq forma maydonlarini guruhlash.
- `button` va `input type="submit"` orasidagi farqni tushunish.
- Ichki tekshiruvni sozlash: `min`, `max`, `pattern`, `maxlength`.

---

## Dars vaqti bloklari

| Blok                                    | Mazmuni                            |
| --------------------------------------- | --------------------------------- |
| 1. select, option, optgroup             | Ochiladigan ro'yxatlar             |
| 2. textarea                             | Ko'p qatorli matn                 |
| 3. fieldset va legend                   | Forma maydonlarini guruhlash      |
| 4. Mini-vazifa                           | Selectni mustaqil yig'ish         |
| 5. button vs input type="submit"        | Forma yuborish, yondashuv farqi   |
| 6. Tekshiruv: min/max/pattern/maxlength | Ichki ma'lumot tekshiruvi         |
| 7. Xulosalar va amaliy vazifa           | To'liq ro'yxatdan o'tish formasini yig'ish |

---

## 1-blok. `select`, `option`, `optgroup`

**Oddiy qilib aytganda:** agar o'tgan darsdagi `radio` tugmalari 2-4 ta variant uchun yaxshi bo'lsa, variantlar ko'p bo'lganda (masalan, mamlakatlar yoki shaharlar ro'yxati) radio tugmalar ekranda juda ko'p joy egallaydi. Bunday holat uchun ochiladigan ro'yxat mavjud - faqat bosilganda ochiladigan ixcham ro'yxat.

```html
<label for="city">Shahar:</label>
<select id="city" name="city">
    <option value="tashkent">Toshkent</option>
    <option value="almalyk">Almalyk</option>
    <option value="samarkand">Samarqand</option>
    <option value="bukhara">Buxoro</option>
</select>
```

Teglarni tahlil qilamiz:

- **`<select>`** - butun ochiladigan ro'yxatning qobig'i, majburiy `name` (serverga yuborish uchun) va `id` (`label` bilan bog'lash uchun) bilan.
- **`<option>`** - ro'yxat ichidagi har bir alohida variant. `value` atributi - serverga yuboriladigan narsa, teglar orasidagi ko'rinadigan matn - foydalanuvchi ko'radigan narsa.

### `selected` orqali boshqa qiymat belgilash

```html
<select id="city" name="city">
    <option value="tashkent">Toshkent</option>
    <option value="almalyk" selected>Almalyk</option>
    <option value="samarkand">Samarqand</option>
</select>
```

`selected` atributi (qiymatsiz, o'tgan darsdagi `required` kabi) sahifa yuklanganda foydalanuvchi bosmasdan ko'rsatiladigan variantni belgilaydi.

### `multiple` orqali bir nechta tanlash

```html
<label for="subjects">Fanlarni tanlang (bir nechta bo'lishi mumkin):</label>
<select id="subjects" name="subjects" multiple>
    <option value="html">HTML</option>
    <option value="css">CSS</option>
    <option value="js">JavaScript</option>
</select>
```

`multiple` atributi foydalanuvchiga bir vaqtda bir nechta variantni tanlashga imkon beradi (odatda bosishda Ctrl/Cmd ni ushlab turadi). Bu kamdan-kam uchraydigan, lekin foydali holat - aslida, checkboxlar guruhi uchun vizual alternativa.

### `<optgroup>` - variantlarni guruhlash

Variantlar juda ko'p bo'lganda, ularni nomlangan guruhlarga ajratish mumkin:

```html
<label for="course">Kursni tanlang:</label>
<select id="course" name="course">
    <optgroup label="Frontend">
        <option value="html">HTML</option>
        <option value="css">CSS</option>
        <option value="js">JavaScript</option>
    </optgroup>
    <optgroup label="Backend">
        <option value="php">PHP</option>
        <option value="mysql">MySQL</option>
    </optgroup>
</select>
```

`<optgroup>` mustaqil tanlanadigan variant emas - bu ochiladigan ro'yxat ichidagi vizual sarlavha-ajratgich (qalin, o'zini bosish mumkin emas), `label` atributi ushbu sarlavha matnini belgilaydi.

**O'xshatish:** ko'p `<optgroup>` bilan `<subsection>` bu restoran menyusiga o'xshaydi, "Sho'rvalar", "Issiq taomlar", "Shirinliklar" bo'limlariga bo'lingan - boimlarni tanlab bo'lmaydi, ular faqat ko'p taomlar orasida orientationga yordam beradi.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xato                                                                                | Tuzatish                                                                                                                          |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `<option>` da `value` ni unutish                                                         | `value` bo'lmasa, serverga variantning ko'rinadigan matni yuboriladi - bu ba'zan noqulay (masalan, uzoq matn uchun); `value` ni ongli belgilang |
| Bitta `<select>` da bir nechta `selected` ishlatish `multiple` holda                     | `multiple` bo'lmasa, faqat bitta `<option>` ga `selected` qo'yish mumkin                                                                    |
| `<optgroup>` ni oddiy `<option>` bilan adashtirish, uni bosiladigan variantga aylantirishga harakat qilish | `<optgroup>` faqat vizual guruhlash, o'zi tanlanmaydi                                                                |

---

## 2-blok. `<textarea>` - ko'p qatorli matn

O'tgan darsdagi oddiy `<input type="text">` - bitta qatorli maydon. Uzoq matn kiritish kerak bo'lganda (izoh, xabar, fikr) - `<textarea>` ishlatiladi.

```html
<label for="message">Xabar:</label>
<textarea id="message" name="message" rows="5" cols="40"></textarea>
```

`<input>` dan muhim farqi: **`<textarea>` - juft teg**, juft emas. Boshlang'ich matn (kerak bo'lsa) ochuvchi va yopuvchi teglar orasiga joylashtiriladi, `value` atributiga emas (`textarea` da umuman `value` atributi yo'q):

```html
<textarea id="bio" name="bio" rows="4" cols="40">O'zingiz haqida biroz gapiring...</textarea>
```

**Diqqat:** agar siz aynan kiritishda yo'qoladigan maslahat-pleysxolder (o'tgan darsda tushuntirgandek) istasangiz, teg ichidagi matn emas, `placeholder` atributini ishlating:

```html
<textarea id="bio" name="bio" rows="4" cols="40" placeholder="O'zingiz haqida biroz gapiring..."></textarea>
```

- **`rows`** - maydonning qatorlardagi taxminiy balandligi.
- **`cols`** - maydonning belgilardagi taxminiy kengligi.

Har ikki atribut **dastlabki** o'lchamni belgilaydi - ko'p brauzerlarda foydalanuvchi `textarea` ni o'ng pastki burchakdagi tutqich orqali qo'lda kengaytirishi mumkin.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xato                                                                     | Tuzatish                                                                                                                    |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Boshlang'ich matnni `value="..."` orqali belgilashga harakat qilish                        | `<textarea>` da `value` atributi yo'q - matn ochuvchi va yopuvchi teglar orasiga yoziladi                                        |
| Matn-mazmunini (yuborishda qoladi) va `placeholder` (yo'qoladi) ni adashtirish | Maslahat formati kerak bo'lsa - `placeholder` ishlating; haqiqiy oldindan to'ldirilgan qiymat kerak bo'lsa - uni teglar orasiga yozing |
| Yopuvchi teg `</textarea>` ni unutish                                     | `textarea` - juft teg, maydon dastlab bo'sh bo'lsa ham yopuvchi tegini unutmang                                      |

---

## 3-blok. `<fieldset>` va `<legend>` - forma maydonlarini guruhlash

Forma katta bo'lganda (masalan, bir nechta mantiqiy bo'limli ro'yxatdan o'tish: "Shaxsiy ma'lumotlar", "Aloqa ma'lumotlari", "Parol"), bog'liq maydonlarni vizual va semantik jihatdan birlashtirish foydali.

```html
<fieldset>
    <legend>Shaxsiy ma'lumotlar</legend>

    <label for="firstname">Ism:</label>
    <input type="text" id="firstname" name="firstname"><br>

    <label for="lastname">Familiya:</label>
    <input type="text" id="lastname" name="lastname">
</fieldset>

<fieldset>
    <legend>Aloqa ma'lumotlari</legend>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email"><br>

    <label for="phone">Telefon:</label>
    <input type="text" id="phone" name="phone">
</fieldset>
```

- **`<fieldset>`** - bog'liq maydonlar guruhining qobig'i, brauzer buni odatda guruh atrofida ramka bilan ko'rsatadi.
- **`<legend>`** - ushbu guruhning yorlig'i/sarlavhasi, to'g'ridan-to'g'ri `fieldset` "ramkasi" "ustida" ko'rsatiladi (vizual yuqori chegaraga kiradi).

**Radio guruhlari uchun juda foydali:** bir nechta radio tugma semantik jihatdan bitta "savol" bo'lgani uchun, ularni `fieldset` va `legend` (o'zini savolni belgilovchi) bilan o'rab olish mantiqiy:

```html
<fieldset>
    <legend>Tayyorgarlik darajangiz</legend>

    <input type="radio" id="beginner" name="level" value="beginner">
    <label for="beginner">Boshlang'ich</label><br>

    <input type="radio" id="intermediate" name="level" value="intermediate">
    <label for="intermediate">O'rtacha</label><br>

    <input type="radio" id="advanced" name="level" value="advanced">
    <label for="advanced">Yuqori</label>
</fieldset>
```

**Nima uchun bu oddiy vizual ramkadan muhimroq:** ekran o'quvchisi `fieldset` va `legend` ichidagi radio tugmani o'qiganida, `legend` matnini ham, aniq variantning yorlig'ini ham talaffuz qiladi - masalan, "Tayyorgarlik darajangiz, Boshlang'ich" - bu foydalanuvchiga to'liq kontekst beradi, yolg'iz "Boshlang'ich" so'zi emas, qaysi savolga javob ekanini tushunmasdan.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xato                                                                          | Tuzatish                                                                                          |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `legend` ishlatmasdan `fieldset` ishlatish                                              | `legend` - guruhning majburiy ma'noli qismi, uni o'tkazib yubormang                                      |
| `legend` ni `fieldset` ichida birinchi element qilmash                         | `legend` ochuvchi `<fieldset>` tegidan darhol keyin kelishi kerak                                        |
| Butun formani mantiqiy guruhlarni ajtmasdan `fieldset` bilan o'rab olish | `fieldset` ni faqat mantiqiy maydon bloklari uchun ishlating, "chiroy uchun" emas |

---

## Mini-vazifa

O'zingiz "Mamlakatni tanlang" ochiladigan ro'yxatini yig'ing, uchta variant bilan (O'zbekiston, Qozog'iston, Qirg'iziston), O'zbekiston boshlang'ich tanlangan bo'lsin.

**Yechim:**

```html
<label for="country">Mamlakat:</label>
<select id="country" name="country">
    <option value="uz" selected>O'zbekiston</option>
    <option value="kz">Qozog'iston</option>
    <option value="kg">Qirg'iziston</option>
</select>
```

---

## 5-blok. `button` vs `input type="submit"`

Har ikki element forma yuborishi mumkin, lekin ular orasida muhim farqlar bor.

### `<input type="submit">`

```html
<input type="submit" value="Formani yuborish">
```

Tugmadagi matn `value` atributi orqali belgilanadi (oddiy maydonlarda ko'rgandek). Bu juft teg - ichiga masalan, ikonka boshqa HTML belgilarini qo'yib bo'lmaydi, faqat `value` orqali oddiy matn.

### `<button>`

```html
<button type="submit">Formani yuborish</button>
```

`<button>` - **juft** teg, matn (yoki hatto murakkabroq mazmun - ikonka, ichki teglar) ochuvchi va yopuvchi teglar orasiga joylashtiriladi:

```html
<button type="submit">
    <strong>Yuborish</strong> formasi
</button>
```

### `<button>` dagi `type` atributi - muhim tafsilot

`<button>` da uchta mumkin bo'lgan `type` qiymati bor va bu xatolarning ko'p uchraydigan manbai:

```html
<button type="submit">Yuborish</button>
<button type="reset">Formani tozalash</button>
<button type="button">Oddiy tugma (o'zi hech narsa qilmaydi)</button>
```

- **`type="submit"`** - formani yuboradi (agar `type` aniq ko'rsatilmasa, boshqa qiymat).
- **`type="reset"`** - barcha forma maydonlarini dastlabki qiymatlariga qaytaradi.
- **`type="button"`** - ichki xulqiga ega bo'lmagan oddiy tugma; tugmaning xulqini keyinroq JavaScript orqali qo'shish kerak bo'lganda ishlatiladi (bu kursda biz bunday tugmalarni faol ishlatmaymiz, chunki JavaScript kurs dasturiga kirmaydi, lekin bu qiymatning mavjudligini bilish muhim).

**Muhim ogohlantirish:** agar `<button>` `<form>` ichida va siz `type` ni **aniq ko'rsatmagan bo'lsangiz** - brauzer uni odatda `type="submit"** deb hisoblaydi. Bu kutilmagan forma yuborishiga olib kelishi mumkin, agar siz oddiy "boshqa narsa uchun tugma" qilmoqchi bo'lsangiz. **Qoida: doimo `<button>` da `type` ni aniq ko'rsating.**

---
### Yangi boshlovchilarning ko'p uchraydigan xatolari

| Xato                                                                                                                    | Tuzatish                                                              |
| ------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `<button>` da `type` ko'rsatmaslik, "oddiy tugma" deb kutish                                                         | Doimo `type="submit"`, `type="reset"` yoki `type="button"` ni aniq ko'rsating |
| `input type="submit"` ichiga HTML qo'yishga harakat qilish                                                                        | Murakkab mazmunli tugma kerak bo'lsa — `<button>` ishlating           |
| Aniq kerak bo'lmasdan `type="reset"` ishlatish — foydalanuvchilar ko'p tasodifan bosib, kiritilgan butun matnni yo'qotadi | `reset` ni ehtiyotkorlik bilan ishlating, faqat haqiqatdan kerak bo'lsa |

---

## 6-blok. Ichki tekshiruv: `min`, `max`, `pattern`, `maxlength`

Biz o'tgan darsda tekshiruvni qisman ko'rib chiqdik (`required`, `type="number"` uchun `min`/`max`). Bugun vositalar to'plamini kengaytiramiz.

### `min` va `max` - sonlar va sanalar uchun

```html
<label for="age">Yosh:</label>
<input type="number" id="age" name="age" min="16" max="99">

<label for="event-date">Tadbir sanasi:</label>
<input type="date" id="event-date" name="event-date" min="2026-01-01" max="2026-12-31">
```

Brauzer qiymat ko'rsatilgan chegaralardan tashqariga chiqsa, formani yuborishga ruxsat bermaydi va foydalanuvchiga suzuvchi ogohlantirish ko'rsatadi.

### `maxlength` - matn uzunligini cheklash

```html
<label for="username">Foydalanuvchi nomi (maks. 20 ta belgi):</label>
<input type="text" id="username" name="username" maxlength="20">

<label for="comment">Izoh (maks. 500 ta belgi):</label>
<textarea id="comment" name="comment" maxlength="500"></textarea>
```

`maxlength` ko'rsatilgan miqdordan ortiq belgi kiritishga fizik ruxsat bermaydi - `min`/`max` dan farqli o'laroq, bu yerda oshirib bo'lmaydi, "yuborishda rad etiladi" emas.

### `pattern` - shablon bo'yicha tekshirish (muntazam ifoda)

`pattern` - eng quvvatli, lekin eng murakkab tekshiruv vositasi. U **muntazam ifodalarni** ishlatadi - matn shablonlarini tasvirlovchi maxsus til. Biz bu kursda muntazam ifodalar sintaksisiga chuqur kirmaymiz (bu alohida katta mavzu), lekin bir nechta amaliy misollarni ko'rib chiqamiz.

**Misol: faqat raqamlar, aniq 7 ta belgi (talaba guvohnomasining shartli raqam formati):**

```html
<label for="student-id">Talaba guvohnoma raqami (7 ta raqam):</label>
<input type="text" id="student-id" name="student-id" pattern="[0-9]{7}" title="Aniq 7 ta raqam kiriting">
```

`[0-9]{7}` shablonini tahlil qilish: `[0-9]` "0 dan 9 gacha istalgan raqam" degan ma'noni anglatadi, `{7}` "ketma-ket aniq 7 marta" degan ma'noni anglatadi.

**Misol: ism uchun faqat kirill harflari (raqamlar va lotin harflarisiz):**

```html
<label for="name">Ism (faqat kirill):</label>
<input type="text" id="name" name="name" pattern="[А-Яа-яЁё\s]+" title="Ismni faqat kirill harflari bilan kiriting">
```

**`pattern` yonidagi `title` atributi haqida muhim:** u texnik jihatdan majburiy emas, lekin juda tavsiya etiladi - brauzer tekshiruv xatosida foydalanuvchiga suzuvchi maslahatda aynan `title` dan olingan matnni ko'rsatadi, nima kiritish kerakligini tushuntiradi. `title` bo'lmasa, foydalanuvchi faqat umumiy "Shablonga mos kelma di" ko'radi, bu juda kam foydali.

**Yangi boshlovchilar uchun muhim eslatma:** muntazam ifodalarni chuqur yozish - bu ilg'or ko'nikma, amaliyotda ko'pincha alohida o'rganish yoki tayyor shablonlarni qidirishni talab qiladi (masalan, ma'lum mamlakatning telefon raqamini tekshirish). Bu darsda `pattern` ning asosiy **printsi ini** tushunish muhim, barcha mumkin bo'lgan shablonlarni yod olish emas.

---

### Yangi boshlovchilarning ko'p uchraydigan xatolari

|Xato|Tuzatish|
|---|---|
|`pattern` ni `title` ishlatmasdan ishlatish|Nima kiritish kerakligini tushunarli tushuntirish bilan `title` qo'shing|
|`min`/`max`/`pattern`/`required` ma'lumotlarni 100% himoya qiladi deb kutish (masalan, zararli kiritishdan)|Ichki HTML tekshiruvi - bu foydalanuvchi qulayligi haqida, xavfsizlik haqida emas; haqiqiy ma'lumotlar himoyasi doimo server tomonida ham takrorlanishi kerak (bu kelajak kurslar mavzusi, toza HTML dasturiga kirmaydi)|
|`maxlength` ni haqiqiy ma'lumotlar uchun juda kichik qo'yish (masalan, ism uchun `maxlength="5"`)|Turli misol ma'lumotlar bilan sinab ko'rib, real cheklovlarni ishlab chiqing|

---

## Dars xulosalari

Bugun siz quyidagilarni bilib oldingiz:

- `<select>`/`<option>` ochiladigan ro'yxat yaratadi, `<optgroup>` variantlarni guruhlaydi, `selected` boshqa qiymatni belgilaydi, `multiple` bir nechta variantni tanlashga ruxsat beradi.
- `<textarea>` - ko'p qatorli matn uchun juft teg; boshlang'ich matn teglar orasiga yoziladi, `value` orqali emas.
- `<fieldset>`/`<legend>` bog'liq forma maydonlarini semantik jihatdan guruhlaydi - radio guruhlari uchun juda foydali.
- `<button>` `<input type="submit">` dan moslashuvchanroq - ichki mazmuni qo'llab-quvvatlaydi, lekin `type` ni aniq ko'rsatishni talab qiladi.
- `min`/`max` sonlar va sanalar diapazonini cheklaydi, `maxlength` matn uzunligini cheklaydi, `pattern` shablon bo'yicha tekshiradi (tushunarli maslahat uchun majburiy `title` bilan).
