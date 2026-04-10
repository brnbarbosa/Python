# Bruno's Python Mistakes Log

Last updated: 2026-04-10

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

## Mistake #9 — Calling `load_dotenv()` Inside a Function

**Category:** Structure
**First seen:** 2026-04-01
**Last seen:** 2026-04-01
**Occurrences:** 1

**Description:**
Bruno placed `load_dotenv()` inside `api_query()`, meaning it would be called every time the function runs. Initialization code that runs once at startup belongs at module level, not inside functions.

**Example of the mistake:**
```python
def api_query(origin, destination, date):
    load_dotenv()  # called every time api_query() is called
    API_key = os.getenv("AVIATIONSTACK_KEY")
```

**Why it is wrong:**
`load_dotenv()` is startup/initialization code. Putting it inside a function couples initialization to execution and wastes work on every call.

**The correct pattern:**
```python
load_dotenv()  # module level — runs once when the module is imported

def api_query(origin, destination, date):
    API_key = os.getenv("AVIATIONSTACK_KEY")
```

**Rule to remember:**
Initialization runs once at startup — put it at module level, never inside a function that gets called repeatedly.

---

## Mistake #10 — Mixing URL Query String With `params` Dict

**Category:** Concepts
**First seen:** 2026-04-01
**Last seen:** 2026-04-01
**Occurrences:** 1

**Description:**
Bruno embedded parameters directly in the URL f-string AND passed a `params` dict to `requests.get()` simultaneously. These are two different ways to pass query parameters — mixing them creates duplication and confusion.

**Example of the mistake:**
```python
response = requests.get(
    f"http://api.aviationstack.com/v1/flights?access_key={API_key}&limit=10",
    params={"key": "value"},
)
```

**Why it is wrong:**
`requests` builds the query string from `params` automatically. Hardcoding params in the URL defeats the purpose and can cause duplicated or conflicting parameters.

**The correct pattern:**
```python
response = requests.get(
    "http://api.aviationstack.com/v1/flights",
    params={
        "access_key": API_key,
        "limit": 10,
    },
)
```

**Rule to remember:**
Use `params` dict for all query parameters — let `requests` build the URL. Never mix hardcoded URL params with a `params` dict.

---

## Mistake #11 — Wrong Return Type Annotation

**Category:** Style
**First seen:** 2026-04-02
**Last seen:** 2026-04-02
**Occurrences:** 1

**Description:**
Bruno annotated `select_game()` as `-> str` but the function returns a `dict` from the results list. The return type annotation did not match the actual returned value.

**Example of the mistake:**
```python
def select_game(results) -> str:
    ...
    return results[pick]  # this is a dict, not a str
```

**Why it is wrong:**
Type annotations are a contract. A wrong annotation misleads anyone reading the code (including tools like mypy) about what the function actually returns.

**The correct pattern:**
```python
def select_game(results) -> dict:
    ...
    return results[pick]
```

**Rule to remember:**
Before writing `-> type`, ask: what does the last `return` statement actually produce?

---

## Mistake #12 — Off-by-One in Boundary Check

**Category:** Logic
**First seen:** 2026-04-02
**Last seen:** 2026-04-02
**Occurrences:** 1

**Description:**
Bruno wrote `pick > len(results)` to guard against out-of-bounds index selection. This allows `pick == len(results)` to pass, which is one beyond the last valid index.

**Example of the mistake:**
```python
if pick < 0 or pick > len(results):
    raise ValueError(...)
```

**Why it is wrong:**
For a list of length 3, valid indexes are 0, 1, 2. `len(results)` is 3 — which is not a valid index. The check must reject it.

**The correct pattern:**
```python
if pick < 0 or pick >= len(results):
    raise ValueError(...)
```

**Rule to remember:**
Valid indexes run from `0` to `len(x) - 1`. Use `>= len(x)` to reject everything beyond the last item.

---

## Mistake #14 — Inverted Boolean Comparison

**Category:** Logic
**First seen:** 2026-04-07
**Last seen:** 2026-04-07
**Occurrences:** 1

**Description:**
Bruno wrote `threshold_value <= float(current_price)` to check if the current price is at or below the threshold. This fires when the price is *above* the threshold — the opposite of the intended alert condition.

**Example of the mistake:**
```python
return threshold_value <= float(current_price)  # True when price is HIGH — wrong
```

**Why it is wrong:**
The alert should fire when the current price is a deal — meaning current price is less than or equal to the threshold. The comparison was written backwards.

**The correct pattern:**
```python
return float(current_price) <= threshold_value  # True when price is LOW — correct
```

**Rule to remember:**
Read comparisons out loud before committing. "current price is less than or equal to threshold" → `float(current_price) <= threshold_value`.

---

## Mistake #15 — Wrapping `pd.read_csv()` in `with open()`

**Category:** Concepts
**First seen:** 2026-04-08
**Last seen:** 2026-04-08
**Occurrences:** 1

**Description:**
Bruno opened the CSV file manually with `with open()` and passed the file object `f` to `pd.read_csv()`. pandas handles file opening internally — you pass the path directly.

**Example of the mistake:**
```python
with open(data_file, mode="r", encoding="utf-8") as f:
    data = pd.read_csv(f)
```

**Why it is wrong:**
`pd.read_csv()` accepts a `Path` or string path and manages the file lifecycle itself. Wrapping it in `with open()` adds unnecessary boilerplate and implies pandas can't handle paths, which is false.

**The correct pattern:**
```python
return pd.read_csv(data_file)
```

**Rule to remember:**
pandas I/O functions (`read_csv`, `read_excel`, etc.) take paths directly — never open the file yourself first.

---

## Mistake #16 — Calling String Methods Directly on a pandas Series

**Category:** Concepts
**First seen:** 2026-04-09
**Last seen:** 2026-04-09
**Occurrences:** 1

**Description:**
Bruno called `.strip().lower()` directly on a `pd.Series` object. String methods like `.strip()` and `.lower()` are Python string methods — they don't exist on a Series. pandas exposes them through the `.str` accessor.

**Example of the mistake:**
```python
df["status"].strip().lower() == "overdue"  # AttributeError: Series has no .strip()
```

**Why it is wrong:**
A Series is not a string. You can't call string methods on it directly — you must go through `.str` to apply string operations element-wise.

**The correct pattern:**
```python
df["status"].str.strip().str.lower() == "overdue"
```

**Rule to remember:**
To apply string methods to a Series, always go through `.str` first — `series.str.method()`, not `series.method()`.

---

## Mistake #13 — Catching an Exception That Cannot Occur

**Category:** Structure
**First seen:** 2026-04-06
**Last seen:** 2026-04-06
**Occurrences:** 1

**Description:**
Bruno wrapped `record()` in a `try/except FileNotFoundError` block, but `record()` calls `mkdir(exist_ok=True)` before opening the file — the directory is guaranteed to exist, so `FileNotFoundError` can never be raised.

**Example of the mistake:**
```python
try:
    record_path = record(selected_game)
    print(f"File saved on {record_path}.")
except FileNotFoundError:
    print("File not found.")
```

**Why it is wrong:**
Adding error handling for scenarios that cannot happen adds noise, misleads readers into thinking something dangerous is occurring, and violates the principle of handling only real failure modes.

**The correct pattern:**
```python
record_path = record(selected_game)
print(f"File saved on {record_path}.")
```

**Rule to remember:**
Only catch exceptions that can actually be raised. Before adding a `try/except`, ask: under what real conditions does this exception fire?

---

## Mistake #17 — Multi-Column DataFrame Selection With Single Brackets

**Category:** Concepts
**First seen:** 2026-04-09
**Last seen:** 2026-04-09
**Occurrences:** 1

**Description:**
Bruno tried `df["col1", "col2"]` to select multiple columns. This syntax is invalid — selecting multiple columns requires passing a **list** inside the indexing operator.

**Example of the mistake:**
```python
df["assignor", "drawee", "due_date"]  # TypeError
```

**Why it is wrong:**
`df["x"]` selects one column by name. To select multiple, you must pass a list: the outer `[]` is the indexing operator, the inner `[]` is the list.

**The correct pattern:**
```python
df[["assignor", "drawee", "due_date"]]  # double brackets
```

**Rule to remember:**
Single brackets → one column (Series). Double brackets → multiple columns (DataFrame).

---

## Mistake #18 — Using `.days` Instead of `.dt.days` on a Timedelta Series

**Category:** Concepts
**First seen:** 2026-04-09
**Last seen:** 2026-04-09
**Occurrences:** 1

**Description:**
Bruno called `.days` directly on a Series of timedeltas. `.days` is an attribute of a single `timedelta` object — on a Series you must go through the `.dt` accessor first, just like `.str` for string operations.

**Example of the mistake:**
```python
(pd.Timestamp.today() - df["due_date"]).days  # AttributeError
```

**Why it is wrong:**
A Series is not a single timedelta. `.dt` is the accessor that applies datetime/timedelta attributes element-wise across the whole Series.

**The correct pattern:**
```python
(pd.Timestamp.today() - df["due_date"]).dt.days
```

**Rule to remember:**
String methods on a Series → `.str.method()`. Datetime/timedelta methods on a Series → `.dt.attribute`. Never call them directly.

---

## Mistake #20 — Writing to a File Before Ensuring the Directory Exists

**Category:** Logic
**First seen:** 2026-04-10
**Last seen:** 2026-04-10
**Occurrences:** 1

**Description:**
Bruno called `risk_report()` (which writes a file) before calling `REPORTS.mkdir()`, meaning if the `reports/` directory did not exist, the write would crash with `FileNotFoundError`.

**Example of the mistake:**
```python
def main():
    df = load_portfolio(DATA_FILE)
    overdue_df = analysis.days_overdue(df)
    risk_report(overdue_df, OVERDUE_REPORT)  # writes to REPORTS/ ...
    ...
    REPORTS.mkdir(parents=True, exist_ok=True)  # ... but directory created after
```

**Why it is wrong:**
File I/O always requires the parent directory to exist first. Calling `mkdir` after a write is too late — the write fails before `mkdir` ever runs.

**The correct pattern:**
```python
def main():
    REPORTS.mkdir(parents=True, exist_ok=True)  # guarantee directory first
    ...
    risk_report(overdue_df, OVERDUE_REPORT)     # then write safely
```

**Rule to remember:**
Always `mkdir` before any file write. Directory creation is setup — it belongs at the top, before any I/O.

---

## Mistake #19 — Referencing a Method Without Calling It

**Category:** Syntax
**First seen:** 2026-04-09
**Last seen:** 2026-04-09
**Occurrences:** 1

**Description:**
Bruno wrote `pd.Timestamp.today` without parentheses, referencing the method object instead of calling it. The result is a bound method, not a Timestamp.

**Example of the mistake:**
```python
(pd.Timestamp.today - df["due_date"]).dt.days  # subtracts a method object — TypeError
```

**Why it is wrong:**
Without `()`, Python returns the function object itself. The subtraction fails because you cannot subtract a datetime from a function.

**The correct pattern:**
```python
(pd.Timestamp.today() - df["due_date"]).dt.days
```

**Rule to remember:**
If it's a function or method, it needs `()` to run. A name without `()` is just a reference, not an execution.

---
