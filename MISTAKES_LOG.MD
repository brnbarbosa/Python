# Bruno's Python Mistakes Log

Last updated: 2026-03-23

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
**Last seen:** 2026-03-20
**Occurrences:** 2

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

## Mistake #5 — Flat Dict for Nested Data

**Category:** Structure
**First seen:** 2026-03-20
**Last seen:** 2026-03-20
**Occurrences:** 1

**Description:**
Bruno initially designed the aggregation output as a flat dict mixing type keys and category keys at the same level, losing the relationship between them.

**Example of the mistake:**
```python
{"income": 2700.00, "expenses": 2000.00, "salary": 2700.00, "food": 35.00}
```

**Why it is wrong:**
You cannot tell which type a category belongs to, making it impossible to display per-type category breakdowns correctly.

**The correct pattern:**
```python
{"income": {"salary": 2700.00, "total income": 2700.00}, "expense": {"food": 35.00, "total expense": 35.00}}
```

**Rule to remember:**
When data has a parent-child relationship, the structure must reflect that — use nesting, not a flat key dump.

---

## Mistake #6 — `setdefault` With Non-Zero Default Causing Double-Count

**Category:** Logic
**First seen:** 2026-03-20
**Last seen:** 2026-03-20
**Occurrences:** 1

**Description:**
Bruno used `setdefault(key, float(row["amount"]))` followed by `+= float(row["amount"])`, doubling the value for the first occurrence of a category.

**Example of the mistake:**
```python
result["expense"].setdefault(category_normalized, float(row["amount"]))
result["expense"][category_normalized] += float(row["amount"])
```

**Why it is wrong:**
When the key is new, `setdefault` sets it to the amount, then `+=` adds the amount again — first entry is always doubled.

**The correct pattern:**
```python
result["expense"].setdefault(category_normalized, 0.0)
result["expense"][category_normalized] += float(row["amount"])
```

**Rule to remember:**
Always `setdefault` to `0` (or empty), then always `+=` — never seed with the value itself.

---

## Mistake #7 — Using `setdefault` for Unconditional Assignment

**Category:** Style
**First seen:** 2026-03-20
**Last seen:** 2026-03-20
**Occurrences:** 1

**Description:**
Bruno used `setdefault` to write the type totals at the end of the function, but `setdefault` means "set only if missing." The totals should always be overwritten unconditionally.

**Example of the mistake:**
```python
result["income"].setdefault("total income", total_income)
```

**Why it is wrong:**
`setdefault` is for guaranteeing a key exists with a fallback — not for setting a value you always want to assign.

**The correct pattern:**
```python
result["income"]["total income"] = total_income
```

**Rule to remember:**
Use `setdefault` when the key might already exist and you want to preserve it. Use `=` when you always want to set it.

---

## Mistake #8 — Calling `.join()` on a Single String Instead of a List

**Category:** Concepts
**First seen:** 2026-03-23
**Last seen:** 2026-03-23
**Occurrences:** 1

**Description:**
Bruno iterated over a list of lines and called `"\n".join(line)` on each individual string, not on the list itself. Since strings are iterable in Python, `.join()` treated each character as an element, producing garbled output.

**Example of the mistake:**
```python
for line in lines:
    summary += "\n".join(line)  # joins characters of one string, not list items
```

**Why it is wrong:**
`str.join()` takes an iterable of strings. Passing a single string gives you the characters joined by the separator, not the lines.

**The correct pattern:**
```python
summary = "\n".join(lines)  # one call on the whole list
```

**Rule to remember:**
Call `.join()` once on the whole list — never inside a loop on a single item.

---
