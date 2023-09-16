# Lint with Pre-commit

## `pre-commit` 설치
```shell
brew install pre-commit
```

## `pre-commit`을 `git hooks`에 설치
```shell
pre-commit install
```

## `Poetry`를 이용해 `lint` 그룹에 `pre-commit`설치
```shell
poetry add pre-commit --group lint
```

## 아래 설정을 `.pre-commit-config.yaml`에 추가
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
::::{admonition} 주의!
:class: caution
`<< >>` 안의 데이터들은 직접 채워넣어야 합니다.
:::{admonition} 예제
:class: note
```yaml
repos:
  - repo: https://github.com/ambv/black
    rev: 23.7.0
    hooks:
      - id: black
  - repo: https://github.com/PyCQA/isort
    rev: 5.12.0
    hooks:
      - id: isort
  - repo: https://github.com/PyCQA/flake8
    rev: 6.1.0
    hooks:
      - id: flake8
```
:::
::::
