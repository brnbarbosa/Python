# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-06
**Current project:** Track 2 — Steam Deal Monitor
**Current milestone:** Milestone 3 — Monitoring Logic (not started)

---

## Last Session Summary (2026-04-06)

- Added `display_game()` to `display.py` — shows game name, cheapest price, and Steam store link
- Created `record.py` with `.jsonl` append-based storage — saves name, price, and ISO timestamp per query
- Chose `.jsonl` over regular JSON to enable safe, no-read appending for price history
- Fixed filename spaces with `.replace(' ', '_')` for cross-platform safety
- Wired `record()` into `main.py` — app now saves every query result and prints the file path

## Next Session

Start Milestone 3 — monitoring logic: read the `.jsonl` history for a game and detect price drops across queries.



---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.



## Mistakes Log

See `MISTAKES_LOG.md` for the full log (13 entries).

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
| 2026-04-06 | Milestone 2 complete | `display_game()`, `.jsonl` append storage, `datetime.isoformat()`, `json.dumps()`, filename sanitization |
