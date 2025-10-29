---
title: "Python Tooling"
date: "2025-06-06"
description: ""
tags: ["stub"]
draft: false
---

## Dependency management

### uv
```bash
# create a project
uv init 

# add dependency
uv add boto3
uv add "boto3>=@2.38.1"  # in specific version
uv add pytest --dev  # as developer dependency, short for: 'uv add --group dev pytest'

# install dependencies
uv sync  # includes dev group
```

### poetry
```bash
# add dependency
poetry add boto3
poetry add boto3@2.38.1  # in specific version
poetry add moto[dynamodb] --group dev  # as developer dependency

# update dependency
poetry update aiohttp
# update (transitive) dependency to newest version and write lock file
poetry update aiohttp --lock

# remove dependency
poetry remove checkov --group dev
```

### pyenv
```bash
pyenv virtualenvs. # list all virtual environments
pyenv activate <env_name>  # activate environment
pyenv virtualenv-delete <env_name>  # delete environment
```

## Linter / Formatter

### ruff 
...

### pylint 
... 

### black
... 


## Logging
...

## Testing

### pytest
```bash
# executing specific test in a specific folder
pytest ./path/to/folder -k 'name_of_test'

# with coverage (depends on pytest-cov)
pytest --cov=. --cov-report=xml:coverage.xml

# combining multiple coverage files 
COVERAGE_FILE=.coverage.file1 pytest --cov=. --cov-append path/to/test_folder_1 && \
COVERAGE_FILE=.coverage.file2 pytest --cov=. --cov-append path/to/test_folder_2 && \
coverage combine && \
coverage xml -o coverage.xml
```
