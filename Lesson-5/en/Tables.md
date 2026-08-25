## Tables

> **Connection with the previous lesson:** in the last lesson we learned to insert images and media. Today we cover another way to present information — tables, for data that is logically organized into rows and columns.

---

## What you will learn by the end of the lesson

- Build tables with `table`, `tr`, `td`, `th` tags.
- Structure tables using `thead`, `tbody`, `tfoot`.
- Merge cells horizontally and vertically with `colspan` and `rowspan`.
- Make tables accessible to screen readers via `scope` and `caption`.
- Understand when tables are appropriate and when they are not.

---

## Lesson timeline

| Block                                             | Content                                   |
| ------------------------------------------------- | ----------------------------------------- |
| 1. Why tables exist and when NOT to use them      | Tabular data vs page layout               |
| 2. table, tr, td, th                              | Basic table structure                     |
| 3. thead, tbody, tfoot                            | Semantic table division                   |
| 4. Mini-task                                      | Build a simple table                      |
| 5. colspan and rowspan                             | Merging cells                             |
| 6. Table accessibility: caption, scope            | Table caption and header-data association |
| 7. Summary and practical task                     | Reinforcement                             |

---

## Block 1. Why tables exist and when NOT to use them

**In simple terms:** an HTML table is the same thing as a table in Excel or Word: data organized into rows (horizontal lines) and columns (vertical lines), where each cell sits at the intersection of a specific row and a specific column.

**The rule for using tables is very simple:** use `<table>` only when you have **actual tabular data** — that is, data where both the row and the column matter simultaneously. Good examples include:

- a class schedule (day of week × time);
- comparing prices across plans (plan × feature);
- a tournament table (team × points/wins/losses);
- a list of students with grades per subject.

### Important historical warning

Many years ago (in the 1990s and early 2000s), web developers used tables **to lay out entire page layouts** — meaning, simply to position the header, menu, and content in the right places on the screen, with no relation to tabular data whatsoever. This is called **"table layout"**, and today it is **considered outdated and not recommended**, because:

- such code is hard to read and maintain;
- a screen reader encountering `<table>` expects to hear data with row/column headers — not the structure of the entire page, which confuses visually impaired users;
- modern CSS (which we'll learn later in the course) provides far more flexible tools for positioning blocks on a page.

**The rule is simple:** if you just want to "position blocks side by side" (e.g., header at the top, menu on the left, content on the right) — that's a CSS job, not `<table>`. Tables are only for actual tabular **data**.

---

## Block 2. `table`, `tr`, `td`, `th`

### Basic structure

```html
<table>
    <tr>
        <th>Name</th>
        <th>Age</th>
        <th>City</th>
    </tr>
    <tr>
        <td>Aziz</td>
        <td>21</td>
        <td>Tashkent</td>
    </tr>
    <tr>
        <td>Dilnoza</td>
        <td>19</td>
        <td>Almalyk</td>
    </tr>
</table>
```

Let's go through each tag.

### `<table>` — the table itself

The outer wrapper for the entire table. Everything else goes inside it.

### `<tr>` (table row) — a table row

Each horizontal row of the table is a separate `<tr>` tag. In the example above there are three rows: one for column headers and two for data.

### `<th>` (table header) — a header cell

Denotes a cell that is a **header** for a row or column, not regular data. By default the browser renders it bold and centered — but as we learned in lesson 2, what matters is not appearance but meaning: `<th>` tells the browser and screen reader "this is a header, the other cells in this column/row belong to it."

### `<td>` (table data) — a regular data cell

All the remaining cells in the table that contain the actual data (not headers).

**Analogy:** think of a gradebook. The top row with subject names ("Math," "Physics," "History") is `<th>`, and the actual grades in the cells are `<td>`. Similarly, the first column with student names is also `<th>` (row headers), and everything else inside is `<td>`.

### `<th>` isn't just at the top — it can be on the left too

```html
<table>
    <tr>
        <th></th>
        <th>Math</th>
        <th>Physics</th>
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

Here there are headers both at the top (subject names) and on the left (student names) — and the empty `<th></th>` in the top-left corner is simply needed to make the table grid align correctly (this is standard practice for tables with "double" headers).

---

### Common beginner mistakes

| Mistake                                                                     | How to fix                                                                                                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Using `<td>` instead of `<th>` for headers                                 | Row/column headers are always `<th>`, not `<td>` with bold text via other tags                                                                           |
| Forgetting to close `<tr>`, `<td>`, `<th>`                                 | All three tags are paired — don't forget the closing tags                                                                                                |
| Having different numbers of cells in different rows without reason          | Every `<tr>` should contain the same number of cells (`<td>`/`<th>`), unless you're intentionally merging cells via `colspan`/`rowspan` (block 5)       |
| Using `<table>` to position page blocks (header/menu/content)              | For page layout use CSS — tables are only for tabular data                                                                                               |

---

## Block 3. `thead`, `tbody`, `tfoot`

When a table grows larger and more complex, it helps to explicitly divide it into semantic parts — just like in a report there's a "table header," "main data," and "summary row."

```html
<table>
    <thead>
        <tr>
            <th>Product</th>
            <th>Price</th>
            <th>Quantity</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Laptop</td>
            <td>8,000,000 so'm</td>
            <td>1</td>
        </tr>
        <tr>
            <td>Mouse</td>
            <td>150,000 so'm</td>
            <td>2</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Total</td>
            <td>8,300,000 so'm</td>
            <td>3</td>
        </tr>
    </tfoot>
</table>
```

- **`<thead>`** (table head) — the table header, usually row(s) with column headers.
- **`<tbody>`** (table body) — the main "body" of the table where the data lives. If the table is long (many rows), `<thead>` can sometimes be pinned to the top while `<tbody>` scrolls — this is configured via CSS, but the semantic division is the foundation for this behavior.
- **`<tfoot>`** (table foot) — the table footer, usually for totals (sum, average).

**Important:** these are not mandatory tags (a simple table from block 2 without them is still fully valid), but for tables with real data it's a good practice that explicitly communicates the table's structure to the browser and screen reader.

---

### Common beginner mistakes

| Mistake                                                                         | How to fix                                                                                                                                                                                             |
| ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Placing column headers inside `<tbody>` instead of `<thead>`                    | Header row(s) go in `<thead>`, data goes in `<tbody>`                                                                                                                                                 |
| Writing `<tfoot>` after `<tbody>` in code, expecting it to render below         | Per the spec, `<tfoot>` can be placed before or after `<tbody>` in code — the browser will still render it at the bottom of the table, but for code readability the convention is `thead → tbody → tfoot` |

---

## Mini-task

Build a simple 2-day schedule table on your own, without peeking at the examples: columns "Day" and "Subject," using `<thead>` and `<tbody>`.

**Solution:**

```html
<table>
    <thead>
        <tr>
            <th>Day</th>
            <th>Subject</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Monday</td>
            <td>Math</td>
        </tr>
        <tr>
            <td>Tuesday</td>
            <td>Physics</td>
        </tr>
    </tbody>
</table>
```

---

## Block 5. `colspan` and `rowspan` — merging cells

Sometimes a cell needs to "stretch" across multiple columns or rows — for example, a header that applies to two columns at once.

### `colspan` — horizontal merge (columns)

```html
<table>
    <tr>
        <th colspan="2">Contact information</th>
    </tr>
    <tr>
        <td>Email</td>
        <td>info@saydullayev.fun</td>
    </tr>
    <tr>
        <td>Phone</td>
        <td>+998 90 123-45-67</td>
    </tr>
</table>
```

`colspan="2"` means "this cell takes up the width of two regular cells" — so in the first row there's only one `<th>`, but it visually stretches across the full width of the table (replacing 2 cells).

**Analogy:** imagine a grid sheet where you erase the border between two adjacent cells and write one piece of text across the merged space — that's exactly what `colspan` does.

### `rowspan` — vertical merge (rows)

```html
<table>
    <tr>
        <th>Name</th>
        <th>Subject</th>
        <th>Grade</th>
    </tr>
    <tr>
        <td rowspan="2">Aziz</td>
        <td>Math</td>
        <td>5</td>
    </tr>
    <tr>
        <td>Physics</td>
        <td>4</td>
    </tr>
</table>
```

`rowspan="2"` means "this cell takes up the height of two rows" — so the name "Aziz" isn't repeated twice, it appears once alongside both of his grades.

**Important rule when using `colspan`/`rowspan`:** once you merge a cell across multiple columns/rows, that row/column must contain **fewer** regular cells — exactly as many fewer as the merged cell consumed. In the `rowspan="2"` example, the second `<tr>` contains only 2 cells (`<td>Physics</td><td>4</td>`), not 3 — because the first cell's spot is already "taken" by the merged cell from the first row.

---

### Common beginner mistakes

| Mistake                                                                  | How to fix                                                                                                                                                                |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Forgetting to reduce cell count in the row/column after merging          | If you used `rowspan="2"` in one row — the next row should have one fewer cell                                                                                           |
| Confusing `colspan` (horizontal, columns) with `rowspan` (vertical, rows) | Remember: col = column → `colspan` stretches across columns (width); row = row → `rowspan` stretches across rows (height)                                                |
| Overusing cell merges in complex tables                                  | Use `colspan`/`rowspan` only when it genuinely simplifies data comprehension — excessive merging complicates both the code and table readability, especially for screen readers |

---

## Block 6. Table accessibility: `caption` and `scope`

### `<caption>` — table caption/title

```html
<table>
    <caption>Weekly class schedule</caption>
    <thead>
        <tr>
            <th>Day</th>
            <th>Subject</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Monday</td>
            <td>Math</td>
        </tr>
    </tbody>
</table>
```

`<caption>` is the first child element inside `<table>` (right after the opening `<table>` tag, before `<thead>`). It gives the table a title — analogous to the heading "Table 1. Class schedule" in a printed document. The screen reader announces `<caption>` before reading the table contents, immediately giving the user an understanding of what the table is about.

### `scope` — associating headers with data

The `scope` attribute on the `<th>` tag explicitly states what this header applies to — a column or a row. This is critically important for screen readers: as the user navigates through data cells, the screen reader can automatically announce the corresponding header, "reminding" the user of the context (e.g., "5, Math grade, for Aziz" — instead of a bare "5").

```html
<table>
    <caption>Student grades</caption>
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Math</th>
            <th scope="col">Physics</th>
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

- `scope="col"` — the header applies to the entire **column** below it.
- `scope="row"` — the header applies to the entire **row** next to it.

**Analogy:** imagine explaining a table to someone over the phone who can't see it. Without `scope` you'd just be listing numbers one after another — meaningless. With `scope` you'd clarify each time "this is Aziz's Math grade" — and that's exactly how a screen reader works thanks to this attribute.

---

### Common beginner mistakes

| Mistake                                                                                                | How to fix                                                                                                                     |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Skipping `<caption>`, relying only on text near the table (e.g., `<h2>` before `<table>`)              | Use `<caption>` inside `<table>` — it's semantically tied to the table, unlike arbitrary adjacent text                       |
| Not specifying `scope` on `<th>`                                                                       | Add `scope="col"` or `scope="row"` — especially important for tables with headers on both rows and columns simultaneously     |
| Not placing `<caption>` as the first element inside `<table>`                                          | `<caption>` must come right after the opening `<table>` tag, before `<thead>`                                                  |

---

## Lesson summary

Today you learned:

- Tables (`<table>`) are for **actual tabular data**, not for page layout — that is an outdated and discouraged practice.
- `<tr>` — row, `<th>` — header cell, `<td>` — data cell.
- `<thead>`, `<tbody>`, `<tfoot>` semantically divide the table into header, body, and footer.
- `colspan` merges cells horizontally (columns), `rowspan` vertically (rows).
- `<caption>` gives the table a title, and `scope="col"`/`scope="row"` on `<th>` associates headers with data for screen readers.
