# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-10
**Current project:** Track 3 — Factoring Portfolio Dashboard — COMPLETE
**Current milestone:** Milestone 5 complete — Overdue Risk Analysis.

---

## Last Session Summary (2026-04-10)

- Wired `risk_report()` into `main.py` — imported the function and added `OVERDUE_REPORT` path constant
- Caught and fixed a directory ordering bug: `risk_report()` was called before `REPORTS.mkdir()`, which would crash if the directory didn't exist
- Ran `main.py` cleanly with no errors or warnings
- Verified `reports/days_overdue.csv` contains correct overdue data (assignor, drawee, due_date, amount, overdue_days)
- Track 3 — Factoring Portfolio Dashboard is complete

## Next Session

Start a new project track — discuss options with Bruno (Track 4 pygame game, or a new direction).



---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.

**Mistakes Log**

See `MISTAKES_LOG.md` for the full log (20 entries).




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
| 2026-04-01 | Track 2 — Milestone 1 (started)  | HTTP basics, `requests`, `.env` security`, `pprint`, API key handling |
| 2026-04-02 | Milestone 1 complete, Milestone 2 (partial) | CheapShark API, list[dict] response, `enumerate`, input validation, `while/try/except` |
| 2026-04-06 | Milestone 2 complete | `display_game()`, `.jsonl` append storage, `datetime.isoformat()`, `json.dumps()`, filename sanitization |
| 2026-04-07 | Milestones 3 & 4 complete | `price_history()`, `price_alert()`, `check_for_threshold()`, `threshold_update()`, read-modify-write JSON, `.exists()`, truthy/falsy, `bool` return pattern |
| 2026-04-08 | Track 3 — Milestone 1 complete | `pandas`, `pd.read_csv()`, DataFrame, module-level path constants, `import pandas as pd` |
| 2026-04-09 | Milestones 2, 3 & 4 complete | boolean indexing, `groupby().sum()`, `pd.concat(keys=)`, `pd.Series`, `matplotlib`, `plt.pie()`, `plt.savefig()` |
| 2026-04-09 (2) | Milestone 5 (partial) | `pd.to_datetime()`, `pd.Timestamp.today()`, `.dt.days`, double-bracket column selection, `index=False` |
| 2026-04-10 | Milestone 5 complete — Track 3 complete | `mkdir` ordering, wiring report functions, pipeline verification |
