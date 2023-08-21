# Lint with Github Actions

### 아래 설정을 `.github/workflows/python_lint.yml`에 추가
`Poetry`를 이용해 `Black`, `isort`, `Flake8`을 각각 실행시키는 설정입니다.
`actions/setup-python`을 이용해 파이썬 라이브러리 설치를 캐싱합니다.
`pull_request` 시에만 동작합니다.
```yaml
name: "Python Lint"

on:
  pull_request

env:
  python-version: << python version >>

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

### contents read 권한
명시적으로 contents read 권한만 주고 싶다면 아래의 설정을 추가합니다.
```yaml
permissions:
  contents: read
```

### 특정 파일 수정 시에만 동작
`python_lint.yml` 파일과 파이썬 디렉토리 폴더가 수정된 `pull_request` 시에만 동작하는 설정입니다.
```yaml
on:
  pull_request:
    paths:
      - ".github/workflows/python_lint.yml"
      - "<< python project location >>/**"
```

### 파이썬 프로젝트 디렉토리 설정
파이썬 프로젝트 디렉토리가 레포지토리의 부분집합일 때 사용합니다.
특히 진부분집합일 때 유용합니다.
```yaml
defaults:
  run:
    working-directory: << python project location >>
```
