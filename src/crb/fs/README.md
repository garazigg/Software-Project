# fs — FS module

Everything that touches files on disk: open, store, write reports and make the ZIP. **The original file is never modified.** Standard library only (`pathlib`, `os`, `shutil`, `json`, `zipfile`).

**Owner:** Ali · **Reviews:** Garazi (G1)

## Files

| File | Functions | Tasks | Tests |
|---|---|---|---|
| `store.py` | `can_open`, `store`, `get_path` | F1, F2 | `tests/test_store.py` |
| `report.py` | `write_report` | F3 | `tests/test_report.py` |
| `bundle.py` | `bundle` | F4 | `tests/test_bundle.py` |

## What to build

### F1 · `can_open(path: str) -> bool`
True if the path exists, is a file, ends in `.tsv` and can be read. False otherwise. **Never raises.**

### F2 · `store(path: str) -> str` and `get_path(resource_id: str) -> str`
- `WORKSPACE = Path("workspace")`
- `store`: creates an 8-character ID (`uuid4().hex[:8]`), creates `workspace/<id>/`, copies the file there with `shutil.copy2`, makes the copy read-only (`stat.S_IREAD`) and writes `workspace/<id>/metadata.json` with **name, size in bytes and date (ISO 8601)**. Returns the ID.
- `get_path`: returns the path of the stored copy; raises `FileNotFoundError` if the ID does not exist.

### F3 · `write_report(data: dict, resource_id: str, name: str = "report") -> str`
Writes `data` to `workspace/<id>/<name>.json` (`indent=2`, `ensure_ascii=False`) and adds a key `"created"` with the date (ISO 8601). Returns the path. Raises `FileNotFoundError` if `workspace/<id>` does not exist. It does not care what the result is: a schema check or an agreement percentage.

### F4 · `bundle(resource_id: str) -> str`
Zips everything in `workspace/<id>/` (TSV copy, `metadata.json`, every `.json` report) into `workspace/<id>.zip` with `ZIP_DEFLATED`. Returns the path. Raises `ValueError` (and creates no ZIP) if the folder does not exist or has no `report.json`.

## Workspace layout

```
workspace/
├── <id>/
│   ├── <original name>.tsv   read-only copy
│   ├── metadata.json
│   ├── report.json
│   └── agreement.json        (only when two files are compared)
└── <id>.zip
```

## Tests
Use `tmp_path` and `monkeypatch.chdir` so tests never write into the real `workspace/`.