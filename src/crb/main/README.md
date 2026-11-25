# main — Main module

Joins all the other modules. **This sprint it only contains empty functions** (the command-line interface is planned for the next sprint). In Sprint 2 the modules are shown together with `scripts/demo.py` (G4).

## Files

| File | What it does | Task | Owner |
|---|---|---|---|
| `cli.py` | Command-line interface: `main(argv) -> int`. Empty for now. | T1 | Garazi |
| `orchestrator.py` | Class `Orchestrator`: calls the modules in order. Empty for now. | T1 | Garazi |

## Functions (empty, `raise NotImplementedError`)

```python
# cli.py
main(argv: list[str] | None = None) -> int

# orchestrator.py
class Orchestrator:
    submit(path: str) -> str            # store the file, return its ID
    check(resource_id: str) -> bool     # run the schema checks
    agree(path_a: str, path_b: str) -> str
    package(resource_id: str) -> str    # report + ZIP
    run(path: str) -> str               # submit -> check -> package
```

## Order of the steps (for the next sprint)

1. `fs.store.can_open(path)` and `fs.store.store(path)` → resource ID
2. `schema.checker.SchemaChecker().check(...)` and `get_issues()`
3. `fs.report.write_report(data, resource_id)`
4. `fs.bundle.bundle(resource_id)` → ZIP path

If the checks find problems, the report and the ZIP are still made.