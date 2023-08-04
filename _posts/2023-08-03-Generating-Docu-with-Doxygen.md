---
title: How to generate a modern looking documenation of c++ code using doxygen and doxygen awsome
date: 2023-08-02 14:00:00 
categories: news,blogging 
tags: doxygen,c++,documentation     # TAG names should always be lowercase
---

What do I need?
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

We will do it as an git submodule and copy the files manually. There are two different themes of doxygen awesome. We will choose the sidebar-only theme, since it is visually more appealing! To optain a good result we need to carefully config the doxyfile with all necessairy information. Since we want to have the variant with search bar and switchable dark / light theme. Some extra addings are important. 

### Configuration file

Doxygen configuration needs to be done in the doxyfile. In our case it is `Vicus.doxyfile`.

```

HTML_EXTRA_STYLESHEET  = doxygen-awesome-css/doxygen-awesome.css \
                         doxygen-awesome-css/doxygen-custom/custom.css \
                         doxygen-awesome-css/doxygen-awesome-sidebar-only.css \
                         doxygen-awesome-css/doxygen-awesome-sidebar-only-darkmode-toggle.css \
                         doxygen-awesome-css/doxygen-custom/custom-alternative.css

HTML_EXTRA_FILES       = doxygen-awesome-css/doxygen-awesome-darkmode-toggle.js \
                         doxygen-awesome-css/doxygen-awesome-fragment-copy-button.js \
                         doxygen-awesome-css/doxygen-awesome-paragraph-link.js \
                         doxygen-awesome-css/doxygen-custom/toggle-alternative-theme.js \
                         doxygen-awesome-css/doxygen-awesome-interactive-toc.js \
                         doxygen-awesome-css/doxygen-awesome-tabs.js

GENERATE_TREEVIEW      = YES # optional. Also works without treeview
DISABLE_INDEX          = NO
FULL_SIDEBAR           = NO
HTML_EXTRA_STYLESHEET  = doxygen-awesome-css/doxygen-awesome.css
HTML_COLORSTYLE        = LIGHT # required with Doxygen >= 1.9.5
SEARCHENGINE           = YES # needs to be there to show the serach box

```

Please mind, that the searchengine needs to be enabled, otherwise the serach box is missing! Also it is wise to specify an folder, where the documentation should be created in.

## Run doxygen to generate the documentation

Finally you can runIn order to generate the documentation you can simply run doxygen with the configuration file

```shell
doxygen <config-file>
```

Afterwards you can publish your documentation to your web server. Just copy the `docs` folder and open `html/index.html`

Have fun with your documentation!