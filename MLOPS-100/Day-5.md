# Task

The xFusionCorp Industries ML team uses a Makefile to orchestrate common tasks—data processing, training, testing, and cleanup. A draft Makefile exists at /root/code/fraud-detection/Makefile, but make all does not complete successfully. Bring the Makefile in line with the team's standard.


Change into /root/code/fraud-detection/ and run make all to observe the current failure.

The corrected Makefile must declare the following six targets and behaviour:

setup – Creates a virtual environment at mlops-venv/ and installs dependencies from requirements.txt;
data – Runs python src/data/process_data.py;
train – Runs python src/models/train.py;
test – Runs pytest tests/;
clean – Recursively removes every __pycache__ directory, removes .pytest_cache, and clears the contents of models/;
all – Runs setup, data, train, and test in that order.
All six target names must be declared as .PHONY so that Make never confuses them with files of the same name.

After your changes, make all must complete without error.

Makefile recipes must be indented with a real tab character, not spaces. Make rejects any recipe that is not tab-indented.


# Solution

Change the Makefile

```sh
# Declare all six targets as phony to avoid file/folder collisions
.PHONY: setup data train test clean all

# Default target runs everything in the strict sequence required by the team
all: setup data train test

# 1. Setup: Creates the venv and installs requirements
setup:
	python3 -m venv mlops-venv
	./mlops-venv/bin/pip install --upgrade pip
	./mlops-venv/bin/pip install -r requirements.txt

# 2. Data: Processes data using the virtual environment's Python binary
data:
	./mlops-venv/bin/python src/data/process_data.py

# 3. Train: Trains the model using the virtual environment's Python binary
train:
	./mlops-venv/bin/python src/models/train.py

# 4. Test: Runs the test suite using the virtual environment's pytest binary
test:
	./mlops-venv/bin/python -m pytest tests/

# 5. Clean: Recursively flushes cache files and clears out model directory contents
clean:
	find . -type d -name "__pycache__" -exec rm -rf {} +
	rm -rf .pytest_cache
	rm -rf models/*

```
