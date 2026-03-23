# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-23
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 2 — Adding Transactions

---

## Last Session Summary (2026-03-23)

- Built `data_summary()` — formats the parsed dict into a clean, human-readable string using `"\n".join(lines)`
- Learned why `.join()` must be called on the whole list, not on individual items inside a loop
- Added ANSI bold formatting to highlight totals in terminal output
- Milestone 1 exit criteria met: `python tracker.py` prints income, expenses, and per-category breakdown cleanly
- Started introduction to Milestone 2 — `argparse` and subcommands

## Next Session

Start Milestone 2: research `argparse` subcommands vs positional/optional arguments, then build `cli.py` with `summary` and `add` subcommands.

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
