# RD-Agent: portable verification records

Full raw logs are retained in the workspace maintenance evidence, not distributed here. Hashes identify those original logs. A successful build or selected test subset does not imply a full test-suite pass. Commands containing <workspace> describe the original execution environment.

[Machine-readable records](verification.json) · [Repository validation summary](../validation.md)

## Executed commands

| Check | Exit | Duration | Command | Outcomes |
| --- | ---: | ---: | --- | --- |
| agent-runtime-no-network | 0 | unrecordeds | `uv run --no-sync python /tmp/trading-rdagent-agent-smoke.py` | See exit status; no test-count assertion. |
| build | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| build-current-layout | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| build-final | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| build-nested-cache-fixed | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| build-portable-env-final | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| build-standard-asyncio-final | 0 | unrecordeds | `uv build` | Successfully built dist/rdagent-1.0.1.dev0.tar.gz<br>Successfully built dist/rdagent-1.0.1.dev0-py3-none-any.whl |
| compileall-portable | 0 | unrecordeds | `uv run --no-sync python -m compileall -q rdagent` | See exit status; no test-count assertion. |
| docker-prerequisite | 0 | unrecordeds | `docker info` | See exit status; no test-count assertion. |
| python-final-sync | 0 | unrecordeds | `uv sync --all-groups --all-extras --python 3.14.8` | See exit status; no test-count assertion. |
| python3148-sync | 0 | unrecordeds | `uv sync --all-groups --all-extras --python 3.14.8` | See exit status; no test-count assertion. |
| python315-lock | 0 | unrecordeds | `uv lock --upgrade --python 3.15` | See exit status; no test-count assertion. |
| python315-sync | 2 | unrecordeds | `uv sync --python 3.15 --all-groups --all-extras` | See exit status; no test-count assertion. |
| tests | 2 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | See exit status; no test-count assertion. |
| tests-context7-standard-asyncio | 1 | unrecordeds | `uv run --no-sync python -m pytest test/oai/test_pydantic.py test/oai/test_prefect_cache.py --tb=short` | See exit status; no test-count assertion. |
| tests-env-current-runtime | 1 | unrecordeds | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | =================== 2 failed, 6 passed, 1 warning in 19.73s ==================== |
| tests-env-file-store | 0 | unrecordeds | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | =================== 8 passed, 1 warning in 391.32s (0:06:31) =================== |
| tests-final-current-layout | 124 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | See exit status; no test-count assertion. |
| tests-final3148 | 1 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | = 28 failed, 214 passed, 25 warnings, 1 error, 316 subtests passed in 505.51s (0:08:25) = |
| tests-full-portable-final | 1 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts --tb=short` | = 20 failed, 222 passed, 24 warnings, 1 error, 316 subtests passed in 564.93s (0:09:24) = |
| tests-full-standard-asyncio-final | 1 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts --tb=short` | = 20 failed, 222 passed, 17 warnings, 1 error, 316 subtests passed in 436.99s (0:07:16) = |
| tests-nested-cache-fixed | 1 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | = 24 failed, 218 passed, 24 warnings, 1 error, 316 subtests passed in 228.11s (0:03:48) = |
| tests-notebook-conf-current | 0 | unrecordeds | `uv run --no-sync pytest test/notebook test/utils/test_conf.py` | ======================== 65 passed, 4 warnings in 3.71s ======================== |
| tests-offline | 0 | unrecordeds | `uv run --no-sync pytest -m offline --ignore test/scripts` | ==== 131 passed, 112 deselected, 17 warnings, 304 subtests passed in 56.12s ==== |
| tests-offline-final3148 | 0 | unrecordeds | `uv run --no-sync pytest --ignore test/scripts -m offline` | ==== 131 passed, 112 deselected, 16 warnings, 304 subtests passed in 13.05s ==== |
| tests-quoted-portable-env | 1 | unrecordeds | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | =================== 3 failed, 5 passed, 1 warning in 20.28s ==================== |
| tests-upgraded-mcp | 124 | unrecordeds | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | See exit status; no test-count assertion. |
