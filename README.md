# tidal-tool-query-lab

`tidal-tool-query-lab` explores cli tools in Python. The repository keeps the core rule set compact, then surrounds it with examples that show how the decisions move.

## Tidal Tool Query Lab Notes

The quickest review path is the verifier first, then the fixtures, then the operations note. That order makes it easy to see whether the code, data, and explanation still agree.

## Why This Exists

This project keeps the domain idea close to the tests. That makes it useful as a reference implementation, a small experiment, or a starting point for a more specialized tool.

## Implementation Notes

The design is intentionally direct: parse or construct a signal, score it, classify it, and verify the expected branch. This makes the repository useful for studying cli tools behavior without needing a service or database unless the language project itself is SQL. The Python code favors standard library tools and direct tests over framework weight.

## Example Scenarios

`pressure` is the first example I would inspect because it lands on the `review` path with a score of 63. The broader file also keeps `degraded` at -61 and `recovery` at 196, which gives the model a useful low-to-high spread.

## Feature Notes

- Uses fixture data to keep argument shape changes visible in code review.
- Includes extended examples for file input, including `recovery` and `degraded`.
- Documents repeatable reports tradeoffs in `docs/operations.md`.
- Runs locally with a single verification command and no external credentials.
- Stores project constants and verification metadata in `metadata/project.json`.

## Local Setup

Install Python and run the commands from the repository root. The project does not need credentials or a hosted service.

## Tests

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/audit.ps1
```

The audit command checks repository structure and README constraints before it delegates to the verifier.

## Code Tour

- `src`: primary implementation
- `tests`: verification harness
- `fixtures`: compact golden scenarios
- `examples`: expanded scenario set
- `metadata`: project constants and verification metadata
- `docs`: operations and extension notes
- `scripts`: local verification and audit commands
- `pyproject.toml`: Python project metadata

## Boundaries

The scoring model is simple by design. More domain-specific behavior should be added through explicit adapters or extra fixture classes rather than hidden constants.

## Roadmap

- Add a comparison mode that shows how decisions change when one signal is adjusted.
- Add a loader for `examples/extended_cases.csv` and promote selected cases into the language test suite.
- Add a short report command that prints the score breakdown for a single scenario.
- Add one more cli tools fixture that focuses on a malformed or borderline input.

## Try It

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/verify.ps1
```

This runs the language-level build or test path against the compact fixture set.
