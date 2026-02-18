# Intro_to_Research_Software_Engineering
Lecture notes of Intro to Research Software Engineering (RSE) Seminar Course

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





