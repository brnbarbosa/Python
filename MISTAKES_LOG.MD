# Bruno's Python Mistakes Log

Last updated: 2026-03-19

---

## Mistake #1 — CSV Module Misconception

**Category:** Concepts
**First seen:** 2026-03-19
**Last seen:** 2026-03-19
**Occurrences:** 1

**Description:**
Bruno believed the `csv` module "opens and writes only .csv files." In reality the `csv` module is a parser — it wraps an already-open file object and handles delimiter splitting, quoted fields, and column mapping. It knows nothing about file extensions.

**Example of the mistake:**
```python
# Bruno's mental model:
# csv module opens files by itself, like open() but for .csv
```

**Why it is wrong:**
`csv.DictReader` takes a file object, not a path — `open()` is always the first step.

**The correct pattern:**
```python
with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.DictReader(f)  # wraps the already-open file
    for row in reader:
        print(row)
```

**Rule to remember:**
`open()` opens files; `csv.DictReader` reads structure from them — two layers, always both.

---

## Mistake #2 — Function Returns Nothing Instead of Data

**Category:** Structure
**First seen:** 2026-03-19
**Last seen:** 2026-03-19
**Occurrences:** 1

**Description:**
`open_csv_file()` iterated over rows and printed them but did not collect or return anything. A function that reads data must return it — the caller decides what to do with it.

**Example of the mistake:**
```python
def open_csv_file(filename: Path):
    with open(filename, "r", encoding="utf-8") as csv_file:
        reader = csv.DictReader(csv_file)
        for row in reader:
            print(row["category"])  # data is printed and lost
```

**Why it is wrong:**
Printing inside a data-loading function mixes concerns and makes the function impossible to reuse or test.

**The correct pattern:**
```python
def open_csv_file(filename: Path) -> list[dict]:
    with open(filename, "r", encoding="utf-8") as csv_file:
        reader = csv.DictReader(csv_file)
        return list(reader)
```

**Rule to remember:**
Data functions return data. Display functions print. Never mix the two.

---

## Mistake #3 — Unnecessary Type Conversion (Path to str)

**Category:** Style
**First seen:** 2026-03-19
**Last seen:** 2026-03-19
**Occurrences:** 1

**Description:**
Bruno wrapped a `Path` object in `str()` before passing it to `open()`, which is unnecessary — `open()` accepts `Path` objects directly since Python 3.6.

**Example of the mistake:**
```python
with open(str(filename), "r", encoding="utf-8") as csv_file:
```

**Why it is wrong:**
Unnecessary conversion adds noise and implies `open()` can't handle `Path`, which is false.

**The correct pattern:**
```python
with open(filename, "r", encoding="utf-8") as csv_file:
```

**Rule to remember:**
`open()` speaks `Path` natively — never convert unless an old library forces you to.

---

## Mistake #4 — `parents[0]` Instead of `.parent`

**Category:** Style
**First seen:** 2026-03-19
**Last seen:** 2026-03-19
**Occurrences:** 1

**Description:**
Bruno used `Path(__file__).resolve().parents[0]` to get the parent directory. `parents[0]` is valid but verbose — `.parent` is the idiomatic shorthand for the immediate parent.

**Example of the mistake:**
```python
ROOT = Path(__file__).resolve().parents[0]
```

**Why it is wrong:**
Not wrong, but non-idiomatic. `parents[0]` is useful when you need grandparent (`parents[1]`) or higher — for the immediate parent, `.parent` is always preferred.

**The correct pattern:**
```python
ROOT = Path(__file__).resolve().parent
```

**Rule to remember:**
Use `.parent` for one level up; use `.parents[n]` only when climbing multiple levels.

---
