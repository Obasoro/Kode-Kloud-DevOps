## Task
The xFusionCorp Industries data science team needs a standardised Python environment for their new ML project. Set up a virtual environment with the required ML libraries on the controlplane host.


Create a Python virtual environment named ml-env under /root/code/ using python3 -m venv.

Activate the environment and install the following packages: numpy, pandas, scikit-learn, and matplotlib.

Generate a requirements.txt file using pip freeze and save it at /root/code/requirements.txt.

## Solution

```sh
# Create the code directory if it doesn't exist
mkdir -p /root/code/

# Create the virtual environment named ml-env
python3 -m venv /root/code/ml-env

# Activate the virtual environment
source /root/code/ml-env/bin/activate

```

```
# Upgrade pip to the latest version
pip install --upgrade pip

# Install the requested machine learning stack
pip install numpy pandas scikit-learn matplotlib

```

```

pip freeze > /root/code/requirements.txt

```


