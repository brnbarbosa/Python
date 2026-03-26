# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-26
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 4 — Refactor to Modules + Error Handling (in progress)

---

## Last Session Summary (2026-03-26)

- Completed Milestone 3: built `reports.py` with `data_summary()`, extracted from `tracker.py`
- Fixed `parsing()` to only include income/expense sections when data exists (avoids empty sections when filtering)
- Built `models.py` with `Transaction` dataclass — replaced raw dicts throughout `tracker.py` and `filters.py`
- Updated all type annotations and dot notation access (`row.category` instead of `row["category"]`)
- Started Milestone 4: identified error handling scenarios (FileNotFound, invalid amount, invalid args)

## Next Session

Continue Milestone 4: implement `try/except` error handling in `open_csv_file()` for `FileNotFoundError`, then handle invalid amount input in `add_transaction()`.

---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.

---

## Mistakes Log

See `MISTAKES_LOG.md` for the full log (8 entries).

---

## Session History

| Date       | Milestone                        | Key Concepts                                      |
|------------|----------------------------------|---------------------------------------------------|
| 2026-03-19 | Milestone 1 — CSV Foundation     | `csv.DictReader`, `pathlib`, file I/O, list[dict] |
| 2026-03-20 | Milestone 1 — Aggregation logic  | Nested dicts, `setdefault`, accumulator pattern   |
| 2026-03-23 | Milestone 1 — Complete           | `str.join()`, display function, ANSI formatting   |
| 2026-03-24 | Milestone 2 — Complete           | `argparse`, subcommands, `add_transaction()`      |
| 2026-03-26 | Milestones 3 & 4 (partial)       | `reports.py`, `models.py`, `Transaction` dataclass, filters wired |
