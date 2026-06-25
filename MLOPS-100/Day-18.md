# Task

The xFusionCorp Industries ML team keeps different dataset and model versions on different Git branches so that the team can roll between versions cleanly. Tag the current state as v1.0, produce a v2-improved branch based on a newer dataset, and confirm that switching back restores the original data.


A project exists at /root/code/fraud-detection/ with a working DVC pipeline and the baseline data/raw/transactions.csv already tracked.

An improved dataset has been pre-staged at /root/code/fraud-detection/data/raw/transactions_v2.csv and is visible in the file explorer. Do not delete this file.

On the main branch, tag the current state as v1.0.

Create a new branch named v2-improved. Replace the tracked dataset with the contents of the v2 file, re-track it with DVC, re-run the pipeline, and commit the changes.

Switch back to the main branch and use dvc checkout to restore the v1 dataset on disk. The restored content must match the hash recorded by the v1.0 tag.

The DVC extension's DVC TRACKED section in the EXPLORER panel will reflect the current branch's tracked state—it should show different dataset hashes on main and v2-improved.

# Solutions

Phase 1: Tag the Baseline State ($v1.0$) on main

```
# Ensure you are on the main branch
git checkout main

# Commit any outstanding tracking files if necessary, then tag
git tag -a v1.0 -m "Baseline dataset and model v1.0"

```

Phase 2: Create v2-improved and Update the Dataset

```
# Create and switch to the new feature branch
git checkout -b v2-improved

# Overwrite the active baseline data with the pre-staged v2 data
# (Using cp keeps the v2 file intact at its original location as requested)
cp data/raw/transactions_v2.csv data/raw/transactions.csv

# Tell DVC to track the updated file and recalculate its md5 hash
dvc add data/raw/transactions.csv

# Re-run the reproduction pipeline to retrain/evaluate with v2 data
dvc repro

# Stage the updated .dvc pointer files and pipeline outputs, then commit
git add data/raw/transactions.csv.dvc dvc.lock
git commit -m "Upgrade pipeline to v2 dataset and update metrics"

```

Phase 3: Roll Back and Restore $v1.0$ Data

```
# Switch back to the main branch (or checkout the tag explicitly)
git checkout main

# Sync the workspace disk state with the Git-tracked DVC metadata
dvc checkout

```
