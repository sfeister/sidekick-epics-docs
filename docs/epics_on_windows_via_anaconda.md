# EPICS on Windows via Anaconda Python

Rather than configuring your own Python environment in Windows, which will involve also keeping track of Windows path variables, etc., I recommend using the Conda package manager for Python.

1. Download and install [Anaconda Individual Edition](https://www.anaconda.com/products/individual).
2. Once installed, open “Anaconda Prompt” (search for it in the start menu). This is just like any command prompt in Windows, except that it keeps you within Anaconda Python environments.
3. Now run these commands to create your own special Python environment in which you can manage your Python modules for Epics. We’ll name the environment “epics” for simplicity.
    a. `conda create --name epics python pip`
	b. `conda activate epics`
	c. `conda install numpy`
	d. `pip install pvapy`
4. Now, whenever you want to run a python script involving pvapy:
    a. Open Anaconda Prompt.
    b. `conda activate epics`
            
Run your python script from within Anaconda Prompt.