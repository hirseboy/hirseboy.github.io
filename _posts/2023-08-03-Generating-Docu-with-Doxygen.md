---
title: How to generate a modern looking documenation of c++ code using doxygen and doxygen awsome
date: 2023-08-02 14:00:00 
categories: news, blogging 
tags: doxygen,c++,documentation     # TAG names should always be lowercase
---

# Important links

Links:
1. [Doxygen awesome](https://jothepro.github.io/doxygen-awesome-css/)
2. [Doxygen](https://www.doxygen.nl/index.html)

# How to do it?

## Generate a configuration file

Doxygen uses a configuration file to determine all of its settings. Each project should get its own configuration file. A project can consist of a single source file, but can also be an entire source tree that is recursively scanned.

To simplify the creation of a configuration file, doxygen can create a template configuration file for you. To do this call doxygen from the command line with the -g option:

```shell
doxygen -g <config-file>
```

where <config-file> is the name of the configuration file. If you omit the file name, a file named Doxyfile will be created. If a file with the name <config-file> already exists, doxygen will rename it to <config-file>.bak before generating the configuration template. If you use - (i.e. the minus sign) as the file name then doxygen will try to read the configuration file from standard input (stdin), which can be useful for scripting.

## Install doxygen awesome

To use the theme when generating your documentation, bring the required CSS and JS files from this repository into your project.

This can be done in several ways:
- manually copying the files
- adding the project as a Git submodule
- adding the project as a npm/xpm dependency
- installing the theme system wide

We will do it as an git submodule and copy the files manually.

There are two different themes of doxygen awesome. We will choose the sidebar-only theme, since it is visually more appealing!

To optain a good result we need to carefully config the doxyfile with all necessairy information. Since we want to have the variant with search bar and switchable dark / light theme. Some extra addings are important.

## Run doxygen to generate the documentation

In order to generate the documentation you can simply run doxygen with the configuration file

```shell
doxygen <config-file>
```