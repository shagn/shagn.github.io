---
title: "Python Tooling"
date: "2025-06-06"
description: ""
tags: ["stub"]
draft: false
---

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

## Dependency management

### uv
```bash
# create a project
uv init 
# add dependency
uv add boto3
uv add "boto3>=@2.38.1"  # in specific version
uv add boto3 --dev  # as developer dependency
```

### poetry
```bash
# add dependency
poetry add boto3
poetry add boto3@2.38.1  # in specific version
poetry add moto[dynamodb] --group dev  # as developer dependency

# update dependency
poetry update aiohttp

# remove dependency
poetry remove checkov --group dev
```

### pyenv
...
