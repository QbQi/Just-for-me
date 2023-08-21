# Lint with Poetry

### Black
#### `Poetry`를 이용해 `lint` 그룹에 `Black`설치
```shell
poetry add black --group lint
```

#### 아래 설정을 `pyproject.toml`에 추가
한 줄에 120자까지 허용하는 설정입니다.
```toml
[tool.black]
line-length = 120
```
:::{admonition} `Black` 설정 더 알아보기
:class: seealso, dropdown
[More Black options](https://black.readthedocs.io/en/stable/usage_and_configuration/the_basics.html#command-line-options)  
[Configuration via a file](https://black.readthedocs.io/en/stable/usage_and_configuration/the_basics.html#configuration-via-a-file)
:::

### isort
#### `Poetry`를 이용해 `lint` 그룹에 `isort`설치
```shell
poetry add isort --group lint
```

#### 아래 설정을 `pyproject.toml`에 추가
`Black`에 호환되는 설정 및 한 줄에 1개의 `import`만 가능하도록 변경하는 설정입니다.
```toml
[tool.isort]
profile = "black"
filter_files = true
force_single_line = true
```
:::{admonition} `isort` 설정 더 알아보기
:class: seealso, dropdown
[Compatibility with Black](https://pycqa.github.io/isort/docs/configuration/black_compatibility.html)  
[Configuration options for isort](https://pycqa.github.io/isort/docs/configuration/options.html)
:::

### Flake8
#### `Poetry`를 이용해 `lint` 그룹에 `Flake8`설치
```shell
poetry add flake8 --group lint
```

#### 아래 설정을 `tox.ini`에 추가
한 줄에 120자까지 허용하는 설정입니다.
:::{admonition} 주의!
:class: caution
`tox.ini`은 레포지토리 최상위 디렉토리에 위치해야 합니다.
:::
```ini
[flake8]
max-line-length = 120
```
:::{admonition} `Flake8` 설정 더 알아보기
:class: seealso, dropdown
[Configuring Flake8](https://flake8.pycqa.org/en/latest/user/configuration.html)
:::
