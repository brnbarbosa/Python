# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-09
**Current project:** Track 3 — Factoring Portfolio Dashboard
**Current milestone:** Milestones 2, 3, and 4 complete.

---

## Last Session Summary (2026-04-09)

- Built `analysis.py` with three functions: `overdue_invoices()`, `total_per_assignor()`, `total_per_drawee()`, `total_per_status()` using pandas boolean indexing and `groupby().sum()`
- Built `reports.py` with `report_totals()` — exports a labeled CSV using `pd.concat()` with `keys` and `to_csv()` with `index_label`
- Built `charts.py` with a reusable `pie_chart()` function using matplotlib — produces PNG files saved to `reports/`
- Wired everything in `main.py` using a dict-driven loop to generate all three charts without repetition
- Full pipeline working: load → analyze → export CSV → export PNG charts

## Next Session

Start Milestone 5 or explore adding more advanced analysis (e.g. overdue amount per assignor, days overdue, average discount rate).



---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences)
`open()` speaks `Path` natively — never convert unless an old library forces you to.

**Mistakes Log**

See `MISTAKES_LOG.md` for the full log (16 entries).




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
