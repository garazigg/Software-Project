# agreement — Agreement module

Compares two annotation files of the **same tokens** (two annotators) and returns the percentage of tokens with the same label. Tokens are matched by `sentence_id` + `token_index`, not by row order.

**Owner:** Marta · **Reviews:** Garazi (G3)

## Files

| File | Functions | Tasks | Tests |
|---|---|---|---|
| `agreement.py` | `match_tokens`, `percentage`, `agree` | A1, A2, A3 | `tests/test_agreement.py` |

## What to build

### A1 · `match_tokens(df_a, df_b) -> DataFrame`
Merge both DataFrames on `["sentence_id", "token_index"]` with suffixes `("_a", "_b")`.
If a token is only in one file, raise `ValueError` saying how many tokens are only in A and only in B (`merge(how="outer", indicator=True)`).
Returns the columns `sentence_id`, `token_index`, `label_a`, `label_b`.

### A2 · `percentage(matched) -> float`
Percentage of rows where `label_a == label_b`, rounded to 2 decimals (e.g. `85.0`).
Empty → `ValueError("No tokens to compare")`.

### A3 · `agree(path_a, path_b) -> float`
Reads both files with `pandas.read_csv(sep="\t", dtype=str, keep_default_na=False)`, then calls `match_tokens` and `percentage`. Returns the percentage.

## Test files (`tests/data/`)
- `annotator_a.tsv` and `annotator_b.tsv`: 10 tokens, 8 with the same label → `80.0`
- A third file with one token less → `agree` raises `ValueError`

## Example

```python
from crb.agreement.agreement import agree
agree("tests/data/annotator_a.tsv", "tests/data/annotator_b.tsv")   # 80.0
```