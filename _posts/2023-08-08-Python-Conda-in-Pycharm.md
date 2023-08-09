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

If some are not found just use the `termina` and install them manually with the conda manager.

```shell
conda install -c conda-forge pythonocc-core
```