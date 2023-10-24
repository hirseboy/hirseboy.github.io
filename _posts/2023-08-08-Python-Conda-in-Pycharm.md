---
title: Using conda in pycharm
date: 2023-08-02 14:00:00 
categories: programming blogging 
tags: python conda documentation     # TAG names should always be lowercase
---


We have had some problems with python packages and were forced to use conda to install packages.

Thats why I am making a short tutorial on how to use it properly.

# How to

First make sure that you have properly installed anaconda or miniconda. In my case I would prefer to install minicoda. In Linux you can do it with some bash commands. 

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

After that you are ready to go. Just restart the terminal and you should first run

```shell
conda install conda
```

In pycharm you can go under `File` > `Settings` to `Interpreter settings`. There you can click `Add Interpreter`

![Add interpreter](/assets/img/add-interpreter.png)

![Conda Environement](/assets/img/conda-interpreter.png)

Choose `Conda environment` and in our case we choose `Create new environment`

Now your can automatically install conda packages in pycharm.

If some are not found just use the `terminal` and install them manually with the conda manager.

Since the conda solver has some slow and buggy solving. It is better to use a new one named `libmamba` 

To install `libmamba` we need to do the following. The libmamba solver’s experimental flag has been removed. 
To use the new solver, update conda in your base environment: 

```shell
conda update -n base conda
```

To install and set the new solver, run the following commands:

```shell
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

Now we can install the pythonOCC-core with:

```shell
conda install -c conda-forge pythonocc-core
```
Since the solver had some problems with this and always froze in the process, we can now install `pythonocc-core` with `libmamba`.

Now we also install `ifctransform` and `pythonocc-utils`

```shell
conda install -c ifcopenshell ifcopenshell 
```

Now comes the tricky part. Since `pythonocc-utils` are not part of the conda repository anymore, we need to build it locally.

First we clone the [repository](https://github.com/tpaviot/pythonocc-utils) of `pythonocc-utils` 

Then we are activating the conda envirement inside the terminal and use pip to manually build the library via the `install.py` in our environement.

```shell
python path/to/setup.py install
```

Now only a GUI-library is missing. We choose to install `PyQt5` via pip since I'm lazy.

```shell
pip install PyQt5
```

Now the python script should run.


