# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-03-20
**Current project:** Track 1 — Personal Finance Tracker CLI
**Current milestone:** Milestone 1 — CSV Foundation

---

## Last Session Summary (2026-03-20)

- Fixed `str(filename)` in `open_csv_file()` — `open()` accepts `Path` directly
- Designed and built `parsing()` — aggregates transactions into a nested `dict[str, dict[str, float]]` by type and category, including per-type totals
- Learned to use `setdefault(key, 0.0)` + `+=` as the correct accumulator pattern
- Collapsed redundant `if/elif` category branches into a single unified block using `type_normalized` as the dict key
- Caught and corrected three logic/style issues through iteration: double-counting with non-zero `setdefault`, unconditional assignment via `setdefault`, and unused `enumerate`

## Next Session

Rename `parsing()` to a descriptive name, replace the manual `append` loop in `open_csv_file()` with `list()`, then build the display function that prints the summary cleanly to the terminal — completing Milestone 1.

---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.

---

## Mistakes Log

See `MISTAKES_LOG.md` for the full log (7 entries).

---

## Session History

| Date       | Milestone                        | Key Concepts                                      |
|------------|----------------------------------|---------------------------------------------------|
| 2026-03-19 | Milestone 1 — CSV Foundation     | `csv.DictReader`, `pathlib`, file I/O, list[dict] |
| 2026-03-20 | Milestone 1 — Aggregation logic  | Nested dicts, `setdefault`, accumulator pattern   |
