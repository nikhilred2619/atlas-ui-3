# PR #1190 validation evidence (archived logs)

This evidence is hosted on a **separate branch of the contributor's fork** to keep binary/test output out of the code PR. It is supplemental to [Sandia PR #1190](https://github.com/sandialabs/atlas-ui-3/pull/1190).

## Archived raw logs

| File | Provenance and outcome |
| --- | --- |
| [Full PR validation log](nov24-full-pr-validation.log) | **November 24, 2026 UTC**, external validation workspace, source `dad0e688` + working-tree review fixes. End-to-end: **63/63 DuckDB** and **75/75 PostgreSQL**; backend suite **6,090 passed, 18 skipped**; PR validation runner **exit 0**. |
| [Full frontend Vitest log](nov24-frontend-full.log) | **November 24, 2026 UTC**, external validation workspace, pre-integration patch: **154 files / 1,957 tests passed**, exit 0. |
| [PostgreSQL migration/concurrency log](nov13-postgresql-migration-concurrency.log) | **November 13, 2026 UTC**, PostgreSQL **16.15**, `ab2fe60b` + working tree: **61 tests passed** in pinning, concurrency, migration and storage. |

**Important provenance note:** These are complete logs from the archived runs at the listed revisions, **not** captured output from the final pushed GitHub commit `d3af77d9`. Please do not attribute them to that exact final commit.

## Additional final-branch local validation reported by contributor

On macOS, **after** integrating upstream main `5ef127d5` and resolving the `conversation_saved` merge conflict, the contributor reported:

- `npx vitest run`: **157 test files, 2,061 tests passed**.
- `TMPDIR=/private/tmp ../.venv/bin/python -m pytest tests -q -n 2 -k "not test_empty_reply_carries_diagnostics_and_is_logged"`: **6,264 passed, 44 skipped, 671 warnings**.
- The excluded `test_empty_reply_carries_diagnostics_and_is_logged` test passed **separately** with `--log-disable=atlas.modules.config.config_loader`. Its full-suite failure was attributed to the substring `hi` occurring in the contributor's local path, rather than the test prompt appearing in LLM logs.
- `TMPDIR=/private/tmp` avoids the macOS `/var` versus `/private/var` resolved-path discrepancy in a separate filename safety test.

These final-branch results were provided as **Terminal summaries**, not newly uploaded raw logs. They are reported as such. GitHub Actions/maintainer review are separate and are not represented by these local runs.

## Evidence handling

The archived logs include test names, synthetic URLs, and dummy fixture credentials as exercised by the public test suite. They are not production credential exports. This branch holds evidence only and does **not** change PR #1190's head/source branch.
