# Module Dependency Map

Import relationships across the `second_brain` project. No circular dependencies detected.

```mermaid
flowchart LR
    subgraph pkg["second_brain (src/)"]
        init["__init__.py"]
        main["__main__.py"]
        app["app.py"]
    end

    subgraph tests["tests/"]
        conftest["conftest.py"]
        test_app["test_app.py"]
    end

    subgraph scripts["scripts/"]
        serve_docs["serve_docs.py"]
    end

    subgraph stdlib["Standard Library"]
        sys["sys"]
        os["os"]
        re["re"]
        subprocess["subprocess"]
    end

    subgraph thirdparty["Third-party"]
        loguru["loguru"]
        pytest["pytest"]
    end

    main      --> app
    test_app  --> app
    app       --> loguru
    app       --> sys
    app       --> os
    conftest  --> pytest
    test_app  --> pytest
    test_app  --> re
    serve_docs --> subprocess
    serve_docs --> sys
```

## Change-safety analysis

| Module | Safe to change? | Dependents |
|---|---|---|
| `app.py` | Carefully — it's the core | `__main__.py`, `tests/test_app.py` |
| `__main__.py` | Yes — only entry-point wiring | none |
| `__init__.py` | Yes — currently empty | none |
| `tests/conftest.py` | Yes — only pytest fixtures | none outside tests |
| `tests/test_app.py` | Yes — leaf node | none |
| `scripts/serve_docs.py` | Yes — standalone script | none |

**No circular dependencies detected.**
