# Task

The xFusionCorp Industries ML team enforces code quality with ruff and black on every pull request. The project at /root/code/fraud-detection/ currently fails both tools. Make it pass them.


The project at /root/code/fraud-detection/ contains a pyproject.toml and sample sources under src/.


The corrected project must meet the following requirements:

ruff and black are both configured with a line length of 120.

ruff lint rule selection includes E, F, W, and I, and is declared under [tool.ruff.lint] – The schema required by ruff 0.1 and later.

Running ruff check src/ from the project directory exits with status 0.

Running black --check src/ from the project directory exits with status 0.

Review the existing configuration and source files, and correct everything that prevents the two commands above from exiting cleanly.

ruff, black, and mypy are already installed. 

# Solution

```sh
[tool.black]
line-length = 120
target-version = ['py310']

[tool.ruff]
line-length = 120

[tool.ruff.lint]
# Select Error (E), Pyflakes (F), Warning (W), and Isort (I) rules
select = ["E", "F", "W", "I"]

```

## For Error

```
ruff check src/ --fix

```

## Test

```
# Verify ruff linting rules pass cleanly
ruff check src/

# Verify black formatting matches perfectly without modifications
black --check src/

```

