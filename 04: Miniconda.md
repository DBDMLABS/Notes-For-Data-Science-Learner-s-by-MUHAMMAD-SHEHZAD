# MINICONDA 
---

## WHAT IS MINICONDA?

> Miniconda is a lightweight distribution of Conda.

It is used to:

    - Create virtual/isolated environments
    - Manage different Python versions
    - Install and manage packages
    - Keep project dependencies isolated
    - Manage Data Science, ML, DL and AI environments


## Remember:
>  Miniconda  ≠  Virtual Environment

> Miniconda provides Conda.

> Conda is used to create and manage environments and packages.


## WHY DO WE USE CONDA?

> Suppose we are working on 3 projects on the same PC:
```bash
My PC
│
├── Project_A/
│   └── code.py
│
├── Project_B/
│   └── code.py
│
└── Project_C/
    └── code.py
```

> Without separate environments:

                    ONE PYTHON
                        │
                        ↓
                ONE PACKAGE ENVIRONMENT
                        │
             ┌──────────┼──────────┐
             ↓          ↓          ↓
         Project A  Project B  Project C


> This can create dependency conflicts.


## EXAMPLE OF PYTHON VERSION CONFLICT


Project A requires:

    Python 3.12

Project B requires:

    Python 3.11

Project C requires:

    Python 3.10


> If all projects use the same environment, managing different Python requirements becomes difficult.


## EXAMPLE OF PACKAGE VERSION CONFLICT

Project A requires:

    pandas 1.x

Project B requires:

    pandas 2.x


> If both projects use the same environment, changing the pandas version for one project may affect the other project.


## SOLUTION — VIRTUAL ENVIRONMENTS

We create separate environments for different projects.

```bash
My PC
│
├── Project_A/
│   ├── code.py
│   └── Environment_A/
│       └── Python + Packages
│
├── Project_B/
│   ├── code.py
│   └── Environment_B/
│       └── Python + Packages
│
└── Project_C/
    ├── code.py
    └── Environment_C/
        └── Python + Packages
```

##  RESULT
```bash
My PC
│
├── Project_A/
│   ├── code.py
│   └── Environment_A/
│       └── Its Python + Packages
│
├── Project_B/
│   ├── code.py
│   └── Environment_B/
│       └── Its Python + Packages
│
└── Project_C/
    ├── code.py
    └── Environment_C/
        └── Its Python + Packages
```

> These environments are isolated, even though all projects are on the same computer.




## EASY FORMULA:

    Folder = Project files
---
    Virtual Environment = Python + Packages
---
    Conda = Environment + Package Manager
---
    Miniconda = Lightweight Conda Distribution


## MINICONDA WITH DIFFERENT TYPES OF PROJECTS

                         MINICONDA
                             │
              ┌──────────────┼──────────────┐
              ↓              ↓              ↓
        Environment 1   Environment 2   Environment 3
        Data Science    Deep Learning    AI Agent
              │              │              │
              ↓              ↓              ↓
           pandas          PyTorch        LangChain
           numpy           Transformers   OpenAI
           sklearn         CUDA tools     FastAPI


> Each environment can have its own:
>      - Python version\
>      - Packages\
>      - Package versions\
>      - Dependencies\
>      - Project configuration


## WHAT IS A CONDA ENVIRONMENT?

A Conda environment is an isolated workspace
where we can install a particular Python version
and packages without affecting other environments.


Example:
```bash
Data Science Environment
│
├── Python 3.12
├── NumPy
├── Pandas
├── Matplotlib
└── Scikit-learn


Deep Learning Environment
│
├── Python 3.11
├── PyTorch
├── Transformers
└── CUDA-related packages


AI Agent Environment
│
├── Python
├── LangChain
├── OpenAI
└── FastAPI
```
## BASIC CONDA COMMANDS


### Check Conda installation

    conda --version



### CREATE A NEW ENVIRONMENT

    conda create -n datascience python=3.12


### Explanation:

    conda create
         ↓
    Create a new environment
---
     -n
        ↓
    Name the environment
---
    datascience
         ↓
    Environment name
---
    python=3.12
      ↓
    Python version
---

### ACTIVATE AN ENVIRONMENT

    conda activate datascience

> After activation:\
>  Python commands and package installations\
>  work inside the datascience environment.


### DEACTIVATE AN ENVIRONMENT

    conda deactivate


> This leaves the currently active environment.


### LIST ALL ENVIRONMENTS

    conda env list


# Example:

> base\
> datascience\
> deeplearning\
> aiagent


> The * indicates the currently active environment.


### INSTALL PACKAGES

    conda install pandas numpy matplotlib


> Packages will be installed into
> the currently active environment.


# 16. REMOVE A PACKAGE

    conda remove pandas
> This removes pandas from the current environment.


### LIST INSTALLED PACKAGES

    conda list


### UPDATE CONDA
    conda update conda


### INSTALL JUPYTER
> conda install jupyter



## COMPLETE DATA SCIENCE ENVIRONMENT

```bash
# Step 1 — Create environment

conda create -n datascience python=3.12


# Step 2 — Activate environment

conda activate datascience


# Step 3 — Install Data Science packages

conda install pandas numpy matplotlib scikit-learn


# Step 4 — Install Jupyter

conda install jupyter


# Step 5 — Start Jupyter Notebook

jupyter notebook

```
---
Author: **MUHAMMAD SHEHZAD**\
GitHub: https://github.com/dbdmlabs
