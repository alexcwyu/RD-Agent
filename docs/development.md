# Development

## Maintained uv environment (2026-10-12)

The tested interpreter selection is Python 3.14.8. uv 0.13.0 resolves runtime dependencies, optional extras, development groups, and build isolation. `uv.lock` records exact versions; `--upgrade` refreshes them within the project and compatibility constraints. Review [validation evidence](validation.md) before treating a build or test command as successful on this host.

Python 3.15 resolution succeeds, but the complete environment cannot install torch 2.14.1 because its available macOS wheels end at CPython 3.14. Python 3.14.8 is the newest tested full environment.

### Layout and build ownership

The upstream rdagent/ package remains flat because scenario workspaces, templates, tooling, and package-relative assets use its established paths. Setuptools discovers all rdagent subpackages. Dependencies remain declared through the upstream requirements files, and uv.lock records exact resolved versions.

Apple Command Line Tools and compiler headers are required when a dependency or extension builds from source.

### Commands from the repository root

```sh
uv python install 3.14.8
uv lock --upgrade --python 3.14.8
uv sync --all-groups --all-extras --python 3.14.8
uv build
uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts
```

### External inputs and test scope

LLM requests, MCP servers, Docker execution, and remote datasets are external boundaries. Model selection and credentials come from settings. Prefect caching optionally persists agent results. A successful package build proves installation, while API and container tests also require the configured services.

Existing upstream skips and xfails remain unchanged. Full suite failures, incomplete runs, and supplemental scoped checks are listed separately in validation. No new test cases were added. The architecture document links existing implementation files and explains the component contracts.

## Portable environment and cache execution

Commands are passed through a quoted shell argument, including nested Python `-c`
programs and complete pipelines. Docker retains its GNU timeout; local execution
uses a deadline on the run's private process group and retains the caller's PATH.
The Qlib Docker configuration opts into the existing MLflow file store with
`MLFLOW_ALLOW_FILE_STORE=true`. User-supplied local volume paths are temporarily
preserved beside the mount and restored after removing only the created symlink.

Workspace hashes exclude `.venv`, `venv`, `.git`, and `__pycache__`. ZIP creation
prunes those directories and the configured cache root, and never includes its own
output archive. Full-restore caches stored inside their own input directory execute
uncached: restoring such a cache would clear the directory containing the cache.
This avoids recursive archive growth and preserves repository and user files.
The generated 547,968,106,600-byte self-archive and its 245-byte marker were removed
by exact path after verification; all other caches and user files were preserved.

API tests need valid chat/embedding credentials and a reachable endpoint. Context7
and Kaggle cases need their actual service credentials and endpoints. The standalone
connectivity script no longer overwrites application credentials during pytest
collection; its existing `test_model(model)` still reports a missing fixture in the
full suite and is retained as a blocker. No network test was skipped or replaced.

Current Pydantic-AI uses `MCPToolset`. Synchronous agent calls preserve the standard asyncio runtime; a caller already inside a notebook event loop uses a private worker thread. The previous global `nest_asyncio` patch made current AnyIO fail to detect its running backend on Python 3.14. The existing Context7 cases are rerun after this repair; remote service and model credentials remain prerequisites.

Set `KG_COMPETITION` to a valid supported Kaggle competition slug before the competition-template integration test; its unset/default value correctly fails the current slug validator. The final complete suite retains this configuration failure, Kaggle authentication failures, remote Context7 connection failures, missing model credentials and the standalone missing pytest fixture.
