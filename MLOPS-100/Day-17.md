# Task
The xFusionCorp Industries data science team compares multiple training runs with different hyperparameters using DVC experiments. Run three experiments that vary the n_estimators hyperparameter, identify the best-performing one, and promote it to the tracked workspace.


A project exists at /root/code/fraud-detection/ with a parameterised DVC pipeline already in place. params.yaml contains n_estimators: 100 and the baseline pipeline has been run once.

Run three DVC experiments, each with a different value for n_estimators across a reasonable range (for example 50, 200, and 500). Each experiment should produce a fresh metrics.json.

Compare the experiments and choose the one whose f1_score is the highest.

Apply the chosen experiment to the workspace so its n_estimators, metrics.json, and models/model.pkl become the tracked state.

The DVC extension's EXPERIMENTS section under the DVC view lists every experiment alongside its parameters and metrics, supports running fresh experiments through the + action, and applies a selected experiment to the workspace from the right-click menu—every operation in this lab can be performed either through the extension UI or with the equivalent dvc exp commands.

# Solution

Step 1: Run the Parameter Experiments

```
cd /root/code/fraud-detection/

# Run Experiment 1 (n_estimators = 50)
dvc exp run -S n_estimators=50

# Run Experiment 2 (n_estimators = 200)
dvc exp run -S n_estimators=200

# Run Experiment 3 (n_estimators = 500)
dvc exp run -S n_estimators=500

```

Step 2: Compare Experiment Performance

```
dvc exp show

```

Step 3: Promote the Winning Run to Your Workspace

```
# Replace 'YOUR_BEST_EXP_NAME' with the actual name/ID of your highest f1_score run
dvc exp apply YOUR_BEST_EXP_NAME

```

Step 4: Verification

```
# Check that params.yaml reflects the winning n_estimators value
cat params.yaml

# Verify your current tracking status matches up
dvc status

```

