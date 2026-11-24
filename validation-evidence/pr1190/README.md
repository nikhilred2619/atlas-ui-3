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

## November 24, 2026 — Exact-commit validation

**Source commit:** `2ef84f314d9316d24dd26b0b78417d6b10675942`

These tests were executed locally on macOS against the exact commit above. The linked logs are redacted copies of the recorded terminal output; original logs are retained locally.

| Validation | Evidence | Result |
| --- | --- | --- |
| Full frontend Vitest | [Frontend log](nov24-2ef84f31-frontend.log) | 157 files, 2,064 tests passed; exit 0 |
| Backend pytest | [Backend log](nov24-2ef84f31-backend.log) | 6,272 passed, 44 skipped; exit 0 |
| Separately executed logging test | [Logging test](nov24-2ef84f31-isolated-logging-test.log) | 1 passed; exit 0 |
| DuckDB end-to-end | [E2E log](nov24-2ef84f31-duckdb-e2e.log) | 63 passed, 0 failed; exit 0 |

The backend suite excluded `test_empty_reply_carries_diagnostics_and_is_logged`, which passed separately with the logging configuration recorded in its log.

The DuckDB E2E run exercised the real backend and mock LLM using the E2E portion of the repository's PR #1169 validation script. Its server-log prompt-text leakage check passed.

**Scope limitations:** PostgreSQL end-to-end and PostgreSQL-specific recovery validation were not rerun against this exact commit because `ATLAS_TEST_POSTGRES_URL` was not configured. Earlier PostgreSQL evidence remains archived separately above.

The logs have been screened for common sensitive-data patterns, and local user-directory paths have been redacted. These are contributor-run validations, not GitHub Actions results or maintainer approval.
