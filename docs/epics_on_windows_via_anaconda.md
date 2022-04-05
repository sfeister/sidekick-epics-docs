---
layout: default
title: EPICS on Windows via Anaconda Python
authors:
    - Scott Feister
---

# EPICS on Windows via Anaconda Python

Rather than configuring your own Python environment in Windows, which will involve also keeping track of Windows path variables, etc., I recommend using the Conda package manager for Python.


Download and install [Anaconda Individual Edition](https://www.anaconda.com/products/individual).

Once installed, open “Anaconda Prompt” (search for it in the start menu). This is just like any command prompt in Windows, except that it keeps you within Anaconda Python environments.

Now run these commands to create your own special Python environment in which you can manage your Python modules for Epics. We’ll name the environment “epics” for simplicity.

```bash
conda create --name epics python pip
conda activate epics
conda install numpy matplotlib
pip install pvapy
pip install pyepics
```

Now, whenever you want to run a python script involving pvapy, you can open Anaconda Prompt, then run `conda activate epics`.
            
In other tutorials, you can explore running python scripts from within Anaconda Prompt.

For example, you may wish to open up a Jupyter Notebook webpage from the `epics` environment. To do so, first open up the Anaconda Prompt, then type:
```bash
conda activate epics
pip install notebook # first time only
jupyter notebook
```

This will open a Jupyter Notebook landing page.