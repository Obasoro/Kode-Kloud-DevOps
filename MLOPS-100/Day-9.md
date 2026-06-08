# Task

The xFusionCorp Industries ML platform team maintains a Cookiecutter template that new ML projects are generated from. A draft template exists at /root/code/mlops-template/, but it does not render. Correct the template and use it to generate a project.


A Cookiecutter template exists at /root/code/mlops-template/. cookiecutter is installed system-wide.

The corrected template must satisfy every one of the following:

The cookiecutter.json declares four variables:
project_name (default my-ml-project)
author (default xFusionCorp)
python_version (default 3.11)
ml_framework with the choices sklearn, pytorch, and tensorflow
The generated requirements.txt logic:
Contains scikit-learn when ml_framework is sklearn
Contains torch when ml_framework is pytorch
Contains tensorflow when ml_framework is tensorflow
The generated README.md content:
Must reference both the project_name and the author from cookiecutter variables.
The template directory structure {{cookiecutter.project_name}}/ must contain:
Files: README.md and requirements.txt
Directories: data/, models/, src/, and tests/
Review the existing template in the VS Code explorer and correct everything that prevents it from rendering.

Once the template renders, generate a project at /root/code/churn-model/:


  ``` cookiecutter /root/code/mlops-template/ -o /root/code/ --no-input project_name=churn-model ml_framework=sklearn```

The generated project must contain a requirements.txt listing scikit-learn and a README.md that mentions xFusionCorp.

## Solution 

`Step 1: Correct the Template Configuration (cookiecutter.json)`

```
{
  "project_name": "my-ml-project",
  "author": "xFusionCorp",
  "python_version": "3.11",
  "ml_framework": ["sklearn", "pytorch", "tensorflow"]
}

```

`Step 2: Establish the Proper Template Directory Structure`

```
# Create the targeted directory layout inside the template folder
mkdir -p /root/code/mlops-template/{{cookiecutter.project_name}}/{data,models,src,tests}

```

`Step 3: Fix the Jinja2 Templating Files`

```
{% if cookiecutter.ml_framework == 'sklearn' %}
scikit-learn
{% elif cookiecutter.ml_framework == 'pytorch' %}
torch
{% elif cookiecutter.ml_framework == 'tensorflow' %}
tensorflow
{% endif %}

```

`Setup Project Metadata (README.md)`

```
# {{ cookiecutter.project_name }}

**Author:** {{ cookiecutter.author }}
**Python Version:** {{ cookiecutter.python_version }}
**ML Framework:** {{ cookiecutter.ml_framework }}

This machine learning project repository was scaffolded using the standard xFusionCorp MLOps template.

```

`Step 4: Generate the Churn Model Project`

```
cookiecutter /root/code/mlops-template/ -o /root/code/ --no-input project_name=churn-model ml_framework=sklearn

```

`Step 5: Final Validation Check`

```
# Verify the generated tree structure matches requirements exactly
find /root/code/churn-model/ -maxdepth 2

# Verify requirements.txt correctly filtered down to scikit-learn
cat /root/code/churn-model/requirements.txt

# Verify README.md displays the churn-model name and xFusionCorp author tag
cat /root/code/churn-model/README.md

```

