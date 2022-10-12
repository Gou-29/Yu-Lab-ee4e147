# EE4E147 server sudo guide

This file suppose that you are very familiar with Linux

## 1. Software Install

Currently, softwares are all installed under `/usr/local/`. The `share` directory is created by matlab kernal in jupyter notebook (cannot change yet), so do not remove them.

Recommendation here is to use build from source as the first choice to install all new stuffs. Only use `apt-get install` as the last choise as we cannot control where it will go.

Make new directories to install new softwares and do not contaminate this parent directory. After installation, configure the path in Modulefiles


## 2. Modules and Modulefiles

Modulefiles are stored in `/usr/share/modules/modulefiles`. Under the directory, make new files and you can manage the path of newly installed things.

## 3. System initialization

System initialize `zsh` now. To add or change it is acheived by edit `/etc/profile`

## 4. Manage Access:

Several thing will happend when you see permission denied (i.e. a non-root user try to install some packages in the base, or even raw conda environment). Open as 777 so they can download and install, and **never forget to shut them**, in most case, to 754 or 755. The color of the directory will change if you do not properly manage them, so please check them in a timely manner.

## 5. New user setup bundle

Located in `/home/Data/.zsh_config`. In user page, we also add module to `.bashrc` to take change of shells into account (i.e. in SoS notebook, the shell is bash)