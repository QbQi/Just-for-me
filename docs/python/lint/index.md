(structure:index)=
# Lint

Black, isort, Flake8을 이용한 Python lint 설정에 대한 내용입니다.
```{note}
Mac에서 PyCharm을 사용해 개발하며, GitHub를 원격 레포지토리로 사용한다는 가정하에 작성되었습니다.
```

```{tableofcontents}
```

## 설치 및 설정 요약
### `pre-commit` 설치
```shell
brew install pre-cimmit
```

### `pre-commit` git hook 적용
```shell
pre-commit install
```

### `lint`관련 파이썬 패키지 설치
```shell
poetry add black isort flake8 pre-commit --group lint
```

### `Black`, `isort` 설정 (`pyproject.toml`)
```toml
[tool.black]
line-length = 120

[tool.isort]
profile = "black"
filter_files = true
force_single_line = true
```

### `Flake8` 설청 (`tox.ini`)
```ini
[flake8]
max-line-length = 120
```

### `pre-commit` 설정
```yaml
repos:
  - repo: https://github.com/ambv/black
    rev: << black version >>
    hooks:
      - id: black
  - repo: https://github.com/PyCQA/isort
    rev: << isort version >>
    hooks:
      - id: isort
  - repo: https://github.com/PyCQA/flake8
    rev: << flake8 version >>
    hooks:
      - id: flake8
```

### GitHub actions 설정 (`.github/workflows/python_lint.yml`)
```yaml
name: "Python Lint"

on:
  pull_request:
    paths:
      - ".github/workflows/python_lint.yml"
      - "<< python project location >>/**"

permissions:
  contents: read

env:
  python-version: << python version >>

defaults:
  run:
    working-directory: << python project location >>

jobs:
  Black:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: pipx install poetry
      - uses: actions/setup-python@v4
        with:
          python-version: ${{ env.python-version }}
          cache: "poetry"
      - run: poetry install
      - run: poetry run black . --check --verbose

  isort:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: pipx install poetry
      - uses: actions/setup-python@v4
        with:
          python-version: ${{ env.python-version }}
          cache: "poetry"
      - run: poetry install
      - run: poetry run isort . --check --verbose

  Flake8:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: pipx install poetry
      - uses: actions/setup-python@v4
        with:
          python-version: ${{ env.python-version }}
          cache: "poetry"
      - run: poetry install
      - run: poetry run flake8 . --verbose
```
