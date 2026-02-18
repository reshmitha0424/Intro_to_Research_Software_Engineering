# Reproducible Environments and Introduction to Containers

## Create Working Directory

```bash
mkdir reproducibility-lecture # Creating a folder 
cd reproducibility-lecture # Changing the directory to the created folder
pwd # Verification of working directory - gives the path of the directory
cd . # . refers to remain in the same directory
```

## Clone the github repository. 
An example repository was taken from https://github.com/mbotto123/reproducible-envs-tutorial.git to clone it. 

```bash
git clone https://github.com/mbotto123/reproducible-envs-tutorial.git
# Repository is cloned. It has reproducible-envs-tutorial folder in it.
cd reproducible-envs-tutorial # Changing directory to reproducible-envs-tutorial folder.
# This folder contains a README.md file, python-example folder and tensor-flow-example folder.
```

## Create a Virtual Environment

```bash
python3 -m venv repro-venv
```
- Python virtual environemnt is created using venv module. 
- In the reproducible-envs-tutorial folder, a new folder "repro-venv" is created, which is a virtual environment folder. 


### Explore the environment structure
```bash
ls repro-venv
# This virtual environemnt folder contains bin, lib and few other folders. 

ls repro-venv/bin
# There is standalone Python interpreter in 'bin'

ls repro-venv/lib/python3.12/site-packages
# Dependensies are stored in 'lib'
```

## Activate the Virtual Environment
```bash
source repro-venv/bin/activate

which python
# Verification of which python interpreter is being used. 
# This python interpreter is used from /reproducibility-lecture/reproducible-envs-tutorial/repro-venv/bin/python
```

## Install the required Packages
```bash
pip install numpy scipy
# These dependencies are installed inside the virtual environment. 
```

## Run the example python script
```bash
cd python-example # Changing directory to python-example folder
python ilu_study.py # Running the python script
```

## Freeze dependencies
- We didn’t specify which versions of the dependencies we want.
- The result of this command will be different in the future.
- One way to address this is to record the package versions in a file.

```bash
cd .. # Change the current working directory to the parent directory (previous one)
pip freeze > requirements.txt # save the installed package versions to requirements.txt file.
# This environemnt can be recreated using <pip install -r requirements.txt>
```

## Deactivate
```bash
deactivate
# The virtual environment is deactivated
```

## Verify Reproducibility

### Create a new environemnt
```bash
python3 -m venv repro-reqs-venv # Create
source repro-reqs-venv/bin/activate # Activate
which python # Now this python interpreter is used from /reproducibility-lecture/reproducible-envs-tutorial/repro-reqs-venv/bin/python
```

### Reinstall dependencies from Requirements file
```bash
pip install -r requirements.txt
# Installs the exact package versions recorded earlier.
```

### Run the python script again
```bash
cd python-example
python ilu_study.py
```
- The script runs successfully in the new environment.
- This confirms that the setup is reproducible.

### Deactivate
```bash
deactivate
```

## Delete the created virtual environments
```bash
cd ..
rm -r repro-venv repro-reqs-venv
# Virtual environments can be easily deleted, but they are deleted permanently.
```

## Is it really reproducible?
- While venv provides Python-level isolation, it has limitations for full reproducibility.
- Specificity is good for reproducibility of the environment, but what if certain versions are no longer available in the future?
- What if the user installs a new version of Python which is incompatible? 
- requirements.txt does not fully capture system-level dependencies

For this, CONDA ENVIRONMENTS can be used. 
- Conda is a bit more general than venv since it can also manage some non-Python packages.
- You get a “base” environment that by default takes precedence over other Python interpreters you have.
- You should still create project-specific environments.
- Consider Miniforge for installation as traditional distributions Anaconda and Miniconda now have licensing restrictions 

## Install CONDA
```bash
# Download Miniforge (x86_64)
wget -O Miniforge3.sh \
  https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh

# Install
bash Miniforge3.sh

# Re-open the terminal or run the below code:
source ~/.bashrc
```

## Conda Environemnt Commands
```bash
# Check if CONDA is available
conda --version

# Create Environment and Install Dependencies
conda create --prefix ./repro-conda numpy scipy

# Activate CONDA
conda activate ./repro-conda

# Capture the Environment
conda export --format=environment-yaml --file=repro-conda.yaml
# This creats a YAML file describing: Python version, NumPy version, SciPy version and ll dependency versions the channels used

# Deactivate
conda deactivate
```

## Difference between Virtual Environment and Conda Environment
- venv only overrides your default Python when the environment is activated, while Conda’s base environment can override the default Python unless reconfigured.
- With venv, you must install and manage different Python versions yourself; Conda allows you to easily specify the Python version directly in the conda create command.
- venv relies on pip to install packages, which is the standard Python approach; Conda manages both Python versions and packages together.
- Conda may have fewer Python packages available compared to pip, but you can still use pip inside a Conda environment if needed.
- Conda generally provides stronger environment isolation and dependency management compared to venv.






