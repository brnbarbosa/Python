# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-02
**Current project:** Track 2 — Steam Deal Monitor
**Current milestone:** Milestone 2 — User Input & Game Selection (in progress)

---

## Last Session Summary (2026-04-02)

- Completed Milestone 1: rewrote `api_client.py` for CheapShark API, made a working game price query by title
- Understood response structure: list of dicts, each with `external`, `cheapest`, `gameID`, `steamAppID`
- Created `display.py` with `get_game_name()` and `select_game()` — user can search and pick a game by number
- Implemented input validation with `while True` / `try/except` and correct `>= len(results)` boundary check
- Wired everything together in `main.py` — app runs end to end but display of selected game data still missing

## Next Session

Complete Milestone 2 by adding a `display_game()` function in `display.py` that prints the selected game's useful fields cleanly to the terminal.



---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.



## Mistakes Log

See `MISTAKES_LOG.md` for the full log (10 entries).

---

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
| 2026-04-01 | Track 2 — Milestone 1 (started)  | HTTP basics, `requests`, `.env` security, `pprint`, API key handling |
| 2026-04-02 | Milestone 1 complete, Milestone 2 (partial) | CheapShark API, list[dict] response, `enumerate`, input validation, `while/try/except` |
