# Python Tutor — Bruno's Learning Journal

## Status

**Last session:** 2026-04-13
**Current project:** Track 4 — Infinite Runner Game (pygame)
**Current milestone:** Milestone 2 complete — gravity, floor clamping, jump mechanic

---

## Track 4 — Infinite Runner Game

**Concept:** A 2D side-scrolling infinite runner. The player jumps over obstacles that approach from the right. The game speeds up over time. Game over on collision.

**Milestones:**
- Milestone 1 — Window, game loop, player rectangle on screen
- Milestone 2 — Gravity and jump mechanic
- Milestone 3 — Obstacles spawning and scrolling
- Milestone 4 — Collision detection and game over screen
- Milestone 5 — Score, speed scaling, restart

## Last Session Summary (2026-04-13)

- Understood gravity as velocity accumulation per frame, not direct position change
- Implemented `GRAVITY` and `player_vertical_velocity` at module level with correct initial values
- Built floor detection using `player.bottom >= HEIGHT` and clamped position with `player.bottom = HEIGHT`
- Debugged jump not working: traced the bug where the `else` block reset velocity immediately after jump — fixed with `elif player_vertical_velocity >= 0`
- Implemented jump on `pygame.KEYDOWN` / `pygame.K_SPACE` with floor guard; tuned `GRAVITY` and `JUMP_FORCE` for fluid feel

## Next Session

Start Milestone 3 — obstacles spawning from the right and scrolling left across the screen.



---

## Top Recurring Mistake

**Mistake #3 — Unnecessary Type Conversion (Path to str)** (2 occurrences) / **Mistake #19 — Referencing a Method Without Calling It** (2 occurrences)

**Mistakes Log**

See `MISTAKES_LOG.md` for the full log (21 entries).




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
| 2026-04-10 (2) | Track 4 — Milestone 1 (partial) | `pygame.init()`, `set_mode()`, `pygame.Rect`, game loop, `pygame.QUIT`, double-buffer rendering, `Clock.tick()` |
| 2026-04-13 | Milestone 2 complete | gravity via velocity accumulation, floor clamping, `pygame.KEYDOWN`, `pygame.K_SPACE`, jump guard with `elif player_vertical_velocity >= 0` |
