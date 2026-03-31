# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-31
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 5 — Automation (complete)

---

## Last Session Summary (2026-03-31)

- Built `report()` in `reports.py` — writes a dated `.txt` report file, creates `reports/` directory with `mkdir(parents=True, exist_ok=True)`, returns the `Path` to the caller
- Added `report` subcommand to `cli.py` and `tracker.py` with `--date` argument (defaults to today via `date.today().isoformat()`) and `strptime` date validation
- Refactored `data.py` — extracted `open_csv_file()` and `parsing()` out of `tracker.py` so both `tracker.py` and `scheduler.py` can import them without circular dependencies
- Built `scheduler.py` — runs `job()` daily at 10:30 using the `schedule` library, with `logging` writing timestamped `.log` files to `logs/`
- Completed Track 1 — Personal Finance Tracker CLI

## Next Session

Start Track 2 — Flight Price Monitor: introduce `requests`, HTTP basics, and querying a public API.



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
| 2026-03-31 | Milestone 5 — Complete           | `pathlib.mkdir`, `schedule`, `logging`, module refactor to `data.py` |
