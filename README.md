# My go-to pre-commit configuration

This is my go-to initial pre-commit configuration when setting up a new project.


## Settings

### pre-commit-hooks:
```
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.3.0
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files
    -   id: mixed-line-ending
```

### black:
```
-   repo: https://github.com/psf/black
    rev: 22.6.0
    hooks:
    -   id: black
```

### isort:
```
-   repo: https://github.com/timothycrosley/isort
    rev: 5.10.1
    hooks:
    -   id: isort
```

### flake8:
```
-   repo: https://gitlab.com/pycqa/flake8
    rev: 3.9.2
    hooks:
    -   id: flake8
```

### mypy:
```
-   repo: https://github.com/pre-commit/mirrors-mypy
    rev: v0.971
    hooks:
        - id: mypy
          additional_dependencies:
            - types-requests
          args:
            - --ignore-missing-imports
```

### pylint
```
-   repo: local
    hooks:
    -   id: pylint
        name: pylint
        entry: pylint
        language: system
        types: [python]
        require_serial: true
        args:
          - --disable=unused-argument,missing-docstring,redefined-outer-name,invalid-name
```


## Example usage in `poetry` project:

Curl `pre-commit-config.yaml` to your project's root directory.

Add `pre-commit` package to your dev dependencies with
```
poetry add pre-commit --dev
```

Run a particular hook on a particular file
```
poetry run pre-commit run <hook_id> --files <file>
```

or all of them on all files
```
poetry run pre-commit run --all-files
```

Make git run your pre-commit hooks automatically before every commit with
```
poetry run pre-commit install
```

Keep the hooks up-to-date with
```
poetry run pre-commit autoupdate
```
