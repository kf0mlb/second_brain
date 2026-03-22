# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

See `README.md` for installation, usage, testing, and docs commands.

## Architecture

All application logic lives in `src/second_brain/app.py`; `__main__.py` is only a one-line entry-point shim.

**Logging** is the main concern of the current codebase:
- `configure_logging()` wires up two loguru sinks: stderr at `LOG_LEVEL` (compact format) and a rotating file at `LOG_FILE` (default loguru format).
- `console_format()` is a callable formatter that maps full level names to 3-letter codes (INF, DBG, etc.). It must explicitly end with `\n{exception}` because loguru callable formatters skip the auto-append.
- Both `LOG_LEVEL` and `LOG_FILE` are read from environment variables; tests override `LOG_FILE` via the `_test_log_file` autouse fixture in `conftest.py` to avoid writing to disk.

**Test environment**: `pytest-env` loads `.env.test` automatically (configured in `pyproject.toml` under `[tool.pytest_env]`). The autouse fixture in `conftest.py` redirects the log file to `tmp_path` for every test.

**Docs**: MkDocs Material with `mkdocstrings` pulling from `src/`. Docstrings should use Google style.
