# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-19
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 1 — CSV Foundation

---

## Last Session Summary

- Set up the project structure and created `PLAN.md` with all 5 milestones
- Designed the CSV schema (`date`, `type`, `category`, `description`, `amount`) and populated `data/transactions.csv` with real data
- Discussed and corrected the misconception that `csv` module opens files — it is a parser that wraps `open()`
- Designed the three-function architecture: `open_csv_file()` → `parsing()` → `display_info()`
- Wrote first version of `tracker.py` with `open_csv_file()` using `csv.DictReader` and `pathlib`

## Next Session

Fix the four issues in `tracker.py` (typo, `str()` conversion, `.parents[0]`, missing return), then write a test file for `open_csv_file()` and move on to implementing `parsing()`.

---

## Top Recurring Mistake

**Mistake #2 — Function Returns Nothing Instead of Data** (1 occurrence)
Data functions must return data. Display functions print. Never mix the two.

---

## Mistakes Log

See `MISTAKES_LOG.MD` for the full log (4 entries).
