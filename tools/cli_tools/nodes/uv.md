# uv

uv is a high-performance Python package manager designed as a replacement for pip and pip-tools.

## Installation

```bash
curl -LsSf 'https://astral.sh/uv/install.sh' | sh
```

### Virtual Environment

```bash
# creat a virtual environment
uv venv
```

## uv pip

```bash
uv pip install pandas
uv pip install -r requirements.txt
uv pip freeze > requirements.txt
uv pip uninstall pandas
uv pip install --upgrade package_name
```

## uv python

> Manage uv python interpreter

```sh
uv python list
uv python install 3.13
uv python uninstall 3.13
# pin project python version
uv python pin 3.13
```

## uv run

> run Python scripts using uv

```sh
uv run main.py
```
