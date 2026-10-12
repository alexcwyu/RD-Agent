# Validation evidence


Current campaign decision: the user explicitly excludes the remaining failing tests from completion requirements. Historical failures below remain failures; they are not relabeled as passes. Source/build/tooling/documentation requirements remain in scope.

Recorded 2026-10-12 on macOS arm64. Selected Python: **3.14.8**; uv0.13.0; native Cargo/Rust1.99.0. Commands below ran from the repository root. Exit124 means the documented time bound expired; exit139 means a native segmentation fault. An earlier failed attempt is retained even if a later rerun succeeds.

## Current scope and result

The complete canonical suite finished:222passed,20failed,1error,316subtests passed; no cases were deselected. Twelve failures require real chat/embedding credentials, two require the configured Context7 MCP endpoint, five require Kaggle authentication, and one requires a valid KG_COMPETITION setting. The existing standalone connectivity test_model(model) has no model fixture and remains an error. All8existing environment cases pass, including real Docker Qlib training, local timeout and mounts. Current MCPToolset and standard asyncio replace removed APIs and an incompatible global nest_asyncio patch. Full suite success is blocked by those explicit prerequisites; package wheel/source builds and runtime controls pass.

Current recorded status: **blocked**. Interpreter fallback evidence and native prerequisites are described in [development](development.md). See [architecture](ayu-develop.md) for workflows, components, and existing source links.

## Executed commands

| Step | Exact command | Exit | Elapsed seconds | Evidence |
|---|---|---:|---:|---|
| python315-lock | `uv lock --upgrade --python 3.15` | 0 | unrecorded | [check record](maintenance/index.html) |
| python315-sync | `uv sync --python 3.15 --all-groups --all-extras` | 2 | unrecorded | [check record](maintenance/index.html) |
| tests | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | 2 | 26.68 | [check record](maintenance/index.html) |
| build | `uv build` | 0 | 7.78 | [check record](maintenance/index.html) |
| tests-upgraded-mcp | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | 124 | 900.04 | [check record](maintenance/index.html) |
| python3148-sync | `uv sync --all-groups --all-extras --python 3.14.8` | 0 | 17.48 | [check record](maintenance/index.html) |
| tests-offline | `uv run --no-sync pytest -m offline --ignore test/scripts` | 0 | 67.52 | [check record](maintenance/index.html) |
| build-final | `uv build` | 0 | 15.24 | [check record](maintenance/index.html) |
| python-final-sync | `uv sync --all-groups --all-extras --python 3.14.8` | 0 | 0.32 | [check record](maintenance/index.html) |
| tests-final3148 | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | 1 | 509.81 | [check record](maintenance/index.html) |
| tests-offline-final3148 | `uv run --no-sync pytest --ignore test/scripts -m offline` | 0 | 17.19 | [check record](maintenance/index.html) |
| docker-prerequisite | `docker info` | 0 | 2.68 | [check record](maintenance/index.html) |
| tests-notebook-conf-current | `uv run --no-sync pytest test/notebook test/utils/test_conf.py` | 0 | 5.53 | [check record](maintenance/index.html) |
| tests-final-current-layout | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | 124 | 600.07 | [check record](maintenance/index.html) |
| build-current-layout | `uv build` | 0 | 5.19 | [check record](maintenance/index.html) |
| build-nested-cache-fixed | `uv build` | 0 | 9.96 | [check record](maintenance/index.html) |
| tests-nested-cache-fixed | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts` | 1 | 232.55 | [check record](maintenance/index.html) |
| tests-quoted-portable-env | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | 1 | 23.15 | [check record](maintenance/index.html) |
| tests-env-current-runtime | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | 1 | 22.71 | [check record](maintenance/index.html) |
| tests-env-file-store | `uv run --no-sync pytest test/utils/test_env.py --tb=short` | 0 | 396.09 | [check record](maintenance/index.html) |
| build-portable-env-final | `uv build` | 0 | 16.71 | [check record](maintenance/index.html) |
| tests-full-portable-final | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts --tb=short` | 1 | 570.3 | [check record](maintenance/index.html) |
| compileall-portable | `uv run --no-sync python -m compileall -q rdagent` | 0 | 0.57 | [check record](maintenance/index.html) |
| tests-context7-standard-asyncio | `uv run --no-sync python -m pytest test/oai/test_pydantic.py test/oai/test_prefect_cache.py --tb=short` | 1 | 8.61 | [check record](maintenance/index.html) |
| tests-full-standard-asyncio-final | `uv run --no-sync python -m coverage run --concurrency=multiprocessing -m pytest --ignore test/scripts --tb=short` | 1 | 440.69 | [check record](maintenance/index.html) |
| build-standard-asyncio-final | `uv build` | 0 | 6.41 | [check record](maintenance/index.html) |
| agent-runtime-no-network | `uv run --no-sync python /tmp/trading-rdagent-agent-smoke.py` | 0 | 6.73 | [check record](maintenance/index.html) |

## Test summaries and failures

### tests

Exit 2; elapsed 26.68seconds.

```text
    class TestPersonModel(BaseModel):

rdagent/scenarios/data_science/dev/runner/__init__.py:29
  /Users/alex/workspaces/trading/RD-Agent/rdagent/scenarios/data_science/dev/runner/__init__.py:29: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.14/migration/
    class DSRunnerCoSTEERSettings(CoSTEERSettings):

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
=========================== short test summary info ============================
ERROR test/oai/test_prefect_cache.py
ERROR test/oai/test_pydantic.py
!!!!!!!!!!!!!!!!!!! Interrupted: 2 errors during collection !!!!!!!!!!!!!!!!!!!!
======================== 7 warnings, 2 errors in 21.27s ========================
```

### tests-upgraded-mcp

Exit 124; elapsed 900.04seconds.

```text
│            │ $entry_exit_code'                                               │
│ Local Path │ /Users/alex/workspaces/trading/RD-Agent/test/utils/tmp_code     │
│ Env        │ PATH::/bin/:/usr/bin/:                                          │
│ Volumes    │ /tmp/full:                                                      │
│            │   /Users/alex/workspaces/trading/RD-Agent/test/utils/tmp_code/… │
└────────────┴─────────────────────────────────────────────────────────────────┘
────────────────────────────── LocalEnv Logs End ───────────────────────────────
2026-10-12 00:19:50.319 | INFO     | rdagent.utils.env:__run_with_retry:341 - Running time: 0.09084415435791016 seconds
2026-10-12 00:19:50.559 | INFO     | rdagent.oai.backend.litellm:_calculate_token_from_messages:68 - [96mToken count: [0m 306
 1 0.09084415435791016
PASSED
test/utils/test_env.py::EnvUtils::test_docker 2026-10-12 00:19:50.717 | INFO     | rdagent.utils.env:prepare:1205 - Building the image from dockerfile: /Users/alex/workspaces/trading/RD-Agent/rdagent/scenarios/qlib/docker
```

### tests-offline

Exit 0; elapsed 67.52seconds.

```text
==== 131 passed, 112 deselected, 17 warnings, 304 subtests passed in 56.12s ====
```

### tests-final3148

Exit 1; elapsed 509.81seconds.

```text
FAILED test/notebook/test_notebook_converter.py::TestNotebookConverter::test_convert
FAILED test/notebook/test_notebook_converter.py::TestNotebookConverter::test_convert_2
FAILED test/notebook/test_util.py::TestSplitCodeAndOutputIntoSections::test_complex
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache - RuntimeErro...
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache_multiprocess
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_multi_round - Runti...
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion_json_mode
FAILED test/oai/test_completion.py::TestChatCompletion::test_json_mode_with_specific_target_type
FAILED test/oai/test_completion.py::TestChatCompletion::test_response_format_with_basemodel
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_list
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_long_text_truncation
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_similarity
FAILED test/oai/test_prefect_cache.py::PydanticTest::test_context7_cache - an...
FAILED test/oai/test_pydantic.py::PydanticTest::test_context7 - anyio._core._...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_data_loader - rdag...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_ensemble - rdagent...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_feature - rdagent....
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_model - rdagent.co...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_workflow - rdagent...
FAILED test/utils/test_agent_infra.py::TestAgentInfra::test_agent_infra - jin...
FAILED test/utils/test_conf.py::ConfUtils::test_ds_costeer_conf - AttributeEr...
FAILED test/utils/test_env.py::EnvUtils::test_conda_error - AssertionError: a...
FAILED test/utils/test_env.py::EnvUtils::test_docker - AssertionError: False ...
FAILED test/utils/test_env.py::EnvUtils::test_docker_mem - AssertionError: Fa...
FAILED test/utils/test_env.py::EnvUtils::test_local - UnicodeDecodeError: 'ut...
FAILED test/utils/test_kaggle.py::TestTpl::test_competition_template - ValueE...
ERROR test/oai/test_llm_connectivity.py::test_model
= 28 failed, 214 passed, 25 warnings, 1 error, 316 subtests passed in 505.51s (0:08:25) =
```

### tests-offline-final3148

Exit 0; elapsed 17.19seconds.

```text
==== 131 passed, 112 deselected, 16 warnings, 304 subtests passed in 13.05s ====
```

### tests-notebook-conf-current

Exit 0; elapsed 5.53seconds.

```text
======================== 65 passed, 4 warnings in 3.71s ========================
```

### tests-final-current-layout

Exit 124; elapsed 600.07seconds.

```text
┌────────────┬─────────────────────────────────────────────────────────────────┐
│ Entry      │ /bin/sh -c 'timeout --kill-after=10 3600 qrun                   │
│            │ /Users/alex/workspaces/trading/RD-Agent/test/utils/env_tpl/con… │
│            │ entry_exit_code=$?; exit $entry_exit_code'                      │
│ Local Path │ .                                                               │
│ Env        │ PATH:/home/v-linlanglv/miniconda3/envs/RD-Agent-310/bin:/bin/:… │
│ Volumes    │ /tmp/full:                                                      │
│            │   /Users/alex/workspaces/trading/RD-Agent/workspace_cache       │
└────────────┴─────────────────────────────────────────────────────────────────┘
/bin/sh: timeout: command not found
────────────────────────────── LocalEnv Logs End ───────────────────────────────
2026-10-12 01:30:34.524 | INFO     | rdagent.utils.env:__run_with_retry:342 - Running time: 0.08170509338378906 seconds
```

### tests-nested-cache-fixed

Exit 1; elapsed 232.55seconds.

```text
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache - RuntimeErro...
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache_multiprocess
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_multi_round - Runti...
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion_json_mode
FAILED test/oai/test_completion.py::TestChatCompletion::test_json_mode_with_specific_target_type
FAILED test/oai/test_completion.py::TestChatCompletion::test_response_format_with_basemodel
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_list
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_long_text_truncation
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_similarity
FAILED test/oai/test_prefect_cache.py::PydanticTest::test_context7_cache - an...
FAILED test/oai/test_pydantic.py::PydanticTest::test_context7 - anyio._core._...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_data_loader - rdag...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_ensemble - rdagent...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_feature - rdagent....
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_model - rdagent.co...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_workflow - rdagent...
FAILED test/utils/test_agent_infra.py::TestAgentInfra::test_agent_infra - jin...
FAILED test/utils/test_env.py::EnvUtils::test_conda_error - AssertionError: a...
FAILED test/utils/test_env.py::EnvUtils::test_docker - AssertionError: False ...
FAILED test/utils/test_env.py::EnvUtils::test_docker_mem - AssertionError: Fa...
FAILED test/utils/test_env.py::EnvUtils::test_local - AssertionError: False i...
FAILED test/utils/test_kaggle.py::TestTpl::test_competition_template - ValueE...
ERROR test/oai/test_llm_connectivity.py::test_model
= 24 failed, 218 passed, 24 warnings, 1 error, 316 subtests passed in 228.11s (0:03:48) =
```

### tests-quoted-portable-env

Exit 1; elapsed 23.15seconds.

```text
FAILED test/utils/test_env.py::EnvUtils::test_conda_error - AssertionError: a...
FAILED test/utils/test_env.py::EnvUtils::test_docker - AssertionError: False ...
FAILED test/utils/test_env.py::EnvUtils::test_local - AssertionError: False i...
=================== 3 failed, 5 passed, 1 warning in 20.28s ====================
```

### tests-env-current-runtime

Exit 1; elapsed 22.71seconds.

```text
FAILED test/utils/test_env.py::EnvUtils::test_docker - AssertionError: False ...
FAILED test/utils/test_env.py::EnvUtils::test_local - PermissionError: [Errno...
=================== 2 failed, 6 passed, 1 warning in 19.73s ====================
```

### tests-env-file-store

Exit 0; elapsed 396.09seconds.

```text
=================== 8 passed, 1 warning in 391.32s (0:06:31) ===================
```

### tests-full-portable-final

Exit 1; elapsed 570.3seconds.

```text
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache - RuntimeErro...
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache_multiprocess
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_multi_round - Runti...
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion_json_mode
FAILED test/oai/test_completion.py::TestChatCompletion::test_json_mode_with_specific_target_type
FAILED test/oai/test_completion.py::TestChatCompletion::test_response_format_with_basemodel
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_list
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_long_text_truncation
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_similarity
FAILED test/oai/test_prefect_cache.py::PydanticTest::test_context7_cache - an...
FAILED test/oai/test_pydantic.py::PydanticTest::test_context7 - anyio._core._...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_data_loader - rdag...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_ensemble - rdagent...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_feature - rdagent....
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_model - rdagent.co...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_workflow - rdagent...
FAILED test/utils/test_agent_infra.py::TestAgentInfra::test_agent_infra - Run...
FAILED test/utils/test_kaggle.py::TestTpl::test_competition_template - ValueE...
ERROR test/oai/test_llm_connectivity.py::test_model
= 20 failed, 222 passed, 24 warnings, 1 error, 316 subtests passed in 564.93s (0:09:24) =
```

### tests-context7-standard-asyncio

Exit 1; elapsed 8.61seconds.

```text
FAILED test/oai/test_pydantic.py::PydanticTest::test_context7 - RuntimeError:...
FAILED test/oai/test_prefect_cache.py::PydanticTest::test_context7_cache - Ru...
```

### tests-full-standard-asyncio-final

Exit 1; elapsed 440.69seconds.

```text
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache - RuntimeErro...
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_cache_multiprocess
FAILED test/oai/test_advanced.py::TestAdvanced::test_chat_multi_round - Runti...
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion
FAILED test/oai/test_completion.py::TestChatCompletion::test_chat_completion_json_mode
FAILED test/oai/test_completion.py::TestChatCompletion::test_json_mode_with_specific_target_type
FAILED test/oai/test_completion.py::TestChatCompletion::test_response_format_with_basemodel
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_list
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_long_text_truncation
FAILED test/oai/test_embedding_and_similarity.py::TestEmbedding::test_embedding_similarity
FAILED test/oai/test_prefect_cache.py::PydanticTest::test_context7_cache - Ru...
FAILED test/oai/test_pydantic.py::PydanticTest::test_context7 - RuntimeError:...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_data_loader - rdag...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_ensemble - rdagent...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_feature - rdagent....
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_model - rdagent.co...
FAILED test/utils/coder/test_CoSTEER.py::CoSTEERTest::test_workflow - rdagent...
FAILED test/utils/test_agent_infra.py::TestAgentInfra::test_agent_infra - Run...
FAILED test/utils/test_kaggle.py::TestTpl::test_competition_template - ValueE...
ERROR test/oai/test_llm_connectivity.py::test_model
= 20 failed, 222 passed, 17 warnings, 1 error, 316 subtests passed in 436.99s (0:07:16) =
```

## Synchronization

All upstream branch and tag refs were fetched by the workspace synchronization procedure. Fork updates use non-forcing pushes; upstream tags also have a private local namespace to preserve divergent tags. The default branch was merged into feature/ayu_develop, preserving the modern package layout and upstream source changes. The workspace synchronization JSON and log retain per-ref outcomes and merge history. This document does not claim that any feature branch was pushed.
