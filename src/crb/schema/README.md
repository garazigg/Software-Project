# schema — Schema module

Checks that an annotated TSV file is correct. Every problem found is an `Issue`.

**Expected columns:** `sentence_id`, `token_index`, `token`, `label` (one token per row).
**Owners:** Olga and Marta · **Reviews:** Garazi (G2)

## Files

| File | What it does | Tasks | Owner | Tests |
|---|---|---|---|---|
| `issue.py` | `Issue(row, column, type, message)` + `to_dict()`. **Already done.** | T1 | Garazi | `tests/test_skeleton.py` |
| `checks.py` | One independent function per check | S1–S5 | Olga, Marta | `tests/test_checks.py` |
| `checker.py` | `SchemaChecker`: runs all the checks | S6 | Olga | `tests/test_checker.py` |

> ⚠️ `checks.py` is **shared**. Each person only fills in the body of their own function, in their own branch and small pull request, so there are no merge conflicts.

## Rows
The header is row 1; the first data row is row 2.

## What to build

### S1 · `read_tsv(path) -> tuple[DataFrame | None, list[Issue]]` — Olga
Read with `pandas.read_csv(path, sep="\t", dtype=str, keep_default_na=False)`.
OK → `(df, [])`. If pandas fails (`ParserError`, `UnicodeDecodeError`, `EmptyDataError`) → `(None, [Issue(0, "", "structure", <reason>)])`.
Test files: `tests/data/valid.tsv` and `tests/data/broken.tsv`.

### S2 · `check_columns(df) -> list[Issue]` — Olga
`EXPECTED_COLUMNS = ["sentence_id", "token_index", "token", "label"]`.
One `column_name` Issue (row 1) per missing or unexpected column; one `column_format` Issue per row where `token_index` is not a whole number.

### S3 · `check_missing(df) -> list[Issue]` — Marta
One `missing_value` Issue ("Empty cell") per cell that is `""` or only spaces. Use pandas operations, not a loop over every cell.

### S4 · `check_duplicates(df) -> list[Issue]` — Olga
Inside each sentence, `token_index` must not repeat. One `duplicate_token` Issue per repeat, using `df.duplicated(subset=["sentence_id", "token_index"])`.

### S5 · `check_labels(df) -> list[Issue]` — Marta
`VALID_LABELS` = the 17 Universal Dependencies UPOS tags (ADJ, ADP, ADV, AUX, CCONJ, DET, INTJ, NOUN, NUM, PART, PRON, PROPN, PUNCT, SCONJ, SYM, VERB, X), to be confirmed with the client.
- Valid after `.strip().upper()` (e.g. `adj`) → `inconsistent_label`, saying the expected label.
- Otherwise (e.g. `FOO`) → `unknown_label`.
- Empty labels are skipped (S3 already reports them).

### S6 · `SchemaChecker` (`checker.py`) — Olga
Only combines the functions of `checks.py` (imports them, does not rewrite them).
- `check(path) -> bool`: empties the list, calls `read_tsv`; if `df` is `None`, keeps its issues and returns `False`; otherwise adds the issues of the four checks and returns `True` if there are none.
- `get_issues() -> list[Issue]`: returns a copy of the list (empty = OK).

Tests replace the five functions with `monkeypatch`, so they do not depend on them.