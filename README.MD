# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-27
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 5 — Automation (in progress)

---

## Last Session Summary (2026-03-27)

- Completed Milestone 4: added `try/except FileNotFoundError` in `main()` with a clear, actionable error message
- Added `try/except ValueError` inside `open_csv_file()` with row number and bad value in the error message
- Confirmed `--amount` validation on CLI is already handled by argparse's `type=float`
- Used `enumerate()` to track row index, with `idx + 2` offset to account for header row
- Started Milestone 5: designed the file-per-report approach (`reports/report_YYYY-MM-DD.txt`), decided `reports.py` owns the write function and redefines `ROOT` internally

## Next Session

Implement the report-to-file function in `reports.py`: takes a date string, builds the path internally using `ROOT`, calls `data_summary()`, and writes the output to a dated `.txt` file.

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
| 2026-03-27 | Milestone 4 — Complete           | `try/except`, `sys.exit()`, `enumerate()`, error handling design  |
