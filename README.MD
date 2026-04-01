# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-01
**Current project:** Track 2 — Steam Deal Monitor
**Current milestone:** Milestone 1 — HTTP Basics & First API Call (in progress)

---

## Last Session Summary (2026-04-01)

- Started Track 2 — pivoted from Flight Price Monitor to Steam Deal Monitor (better fit for Bruno's interests)
- Learned HTTP fundamentals: GET vs POST, status codes, JSON responses, how `requests` works
- Learned API key security: `.env` files, `python-dotenv`, `os.getenv()`, never hardcoding secrets
- Built initial `api_client.py` with `requests.get()` and `params` dict — made a real API call to Aviationstack
- Discovered Aviationstack free tier limitations; evaluated alternatives; chose Steam Deal Monitor
- Set up `flight_monitor/` project structure (to be renamed)

## Next Session

Revisit project goals clearly, rename/restructure project folder for Steam Deal Monitor, pick the right API (IsThereAnyDeal or Steam), and complete Milestone 1 with a working game price query.



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
