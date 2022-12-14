# EE4E147 server user guide

## 0. Linux in 5 minutes
（If you have previous experience, just go to login part and jump to the section 1)

Linux is a kind of operation system (i.e. MacOS, Windows). Unlike other systems you may used now, Linux do not hava a Graphical User Interface (GUI). The may interaction method for you and Linux system is by command. 

Linux tends to be a highly reliable and secure system than any other operating systems, so it is commonly used by scientific computing. 

### 0.1. Login 

As stated, you need use command to access the server. So, command line tools is needed. This is the software **on your own computer** that help us to linke to the server. 

*  Windows user: search a software called `PowerShell` in your PC

*  Mac/Linux user: search a software called `Terminal` in your PC

The appearance of this kind of software will look exactly like that in movies: a black box that allow you to type commands into it. Then, to access server, type (note to change things in <> into your own):
```shell
ssh <YOUR UST USERNAME (i.e. wgouaa) >@ee4e147.ece.ust.hk
```
Similar syntax is used for accessing other servers in our group. Enter your password same as accessing the school email system, and you will logged in.

A quick note on the above command is as follow: in Linux, all command will start with the **software** to be used, and then with **arguments** for that software. Here, `ssh` is the software used and following is the arguments. For each software, always try:

```shell
<SOFTWARE> -h
<SOFTWARE> --help
```

To see the brief introduction of that software and get an insight on how to use it. 

**You are expected to see some instructions to create a file in first way. Please select `(0)`**

### 0.2 What after?

Here, you have entered the Linux system. The location you logged in is your `HOME` directory. It is just like an folder in your onw PC. All of your personal things can be stored into here. Also, others, except users with access (called `root` user), do not have the access to enter this folder.

A main thing you need to learn is how to move from here to there. In linux, we do not have GUI, so to know where you are and where to go is done by command. To begin with, type
```shell
pwd
```

It will tell you your current directory. You are expected to see something like `/home/<YOU UST USERNAME>`, indicate that you are in here. Also, it tells you that you have 2 level of parent directory to reach the very top of the system. Then, type

```shell
cd ..
ls
```
Here, the first command `cd` is to open a certain directory, and `..` indicate the parent directory. The second command `ls` will list things under where you are (after `cd`, you are in `/home`). It will give you lots of UST usernames (and other things), which is all of your labmates' personal folders. To go back your own folder, just type
```shell
cd <YOUR FOLDER NAME>
```
And will leads you back to where we start (use `pwd` to confirm it). The above procedure is similar as clicking here and there in GUI. Then, other essitial things you may want to know include:
* Common commands: A nice tutorial can be found [here](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
* Document manipulation: `vim` or other text editors
* Some basic of shell script `example.sh`
* ... 


#### 0.3 Softwares for better server access:
Except for command line tools, there are bunch of softwares that can help you to interact with server:

* `VScode`: A really hand software for editing. you can refer to this [website](https://code.visualstudio.com/docs/remote/ssh) for setup details
* `MobaXterm`: A windows tool for better server access, also can link GUI between server and you PC (i.e. open matlab in your PC but run code on server)
* `FileZilla`: Specialized in file transfer between server and pc

## 1. Initial setups

### 1.1 Shell configuration

We use `oh-my-zsh` under `zsh` shell for a better experience of command line. Functions like auto suggestion, command auto completion are installed. For your first login, copy following command and run:


**NB1: For previous users in this server, you need to move your settings in `.bashrc` to `.zshrc`. Otherwise do not run the second/third line**

```shell
echo 'source /usr/share/modules/init/bash' >> $HOME/.bashrc
cp /home/Data/.zsh_config/.zshrc $HOME
source $HOME/.zshrc
```

**NB2: If you do want to go back to traditional bash, run `source /bin/bash` and everything will be as usual.**


Then you will see the related change. If you do not like the theme preset, you can edit `.zshrc` file under your home directory by changing the `ZSH_THEME` variable. List of avaiable themes are listed [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes). After change that file, please run 
``` shell
source $HOME/.zshrc
```
Again to allow change. Basically this step tell the server to "save" that change permanatly into `.zshrc` file. You may notice that, if you use `ls` command, you actually do not see this file. This is because the `.` tell linux to hide that document. Similar stratiges are used for folders. To see all the things in a certain directory, you can try `ls -a` of `la` in short. If you go into this file, you may notice that several other setups are in it. This file is the file to be executed each time you log in, so the changes in here will be used each time. 




### 1.2 Login without password

Allow logging in without entering password is a very neat solution for every morning. The basic step here include generate a `key` in your own device and then store the key in the server. You can follow the following steps:


* For Window setup

    - To generate the key, you need to use `PowerShell` and run `ssh-keygen -t rsa`. Type `Enter` for all questions. Then, a key will be generated in your PC at `C:\Users\<username>\.ssh\`. Go into that folder, you will see a file called `id_rsa.pub`. Open that text file and copy the whole key. 

    - Then, you need to edit the accesibility of file `id_rsa.pub`. Right click on that file and enter `Properties/属性(R)`. Go into `Security/安全`. You need to delect all other users except yourself,and set the accessof yourself as read and write only.

    - To send the key to the server, log into the server and create necessary files called `authorized_keys`:
    ```shell
    mkdir .ssh && cd .ssh && touch authorized_keys
    ```
    - After create that file, you need to paste the whole key into that file and save the file.

* For Mac setup, open `Terminal`

    - To generate the key, run `ssh-keygen -t rsa`.
    - To send the key to server, run `ssh-copy-id  ~/.ssh/id_rsa.pub <YOUR UST USERNAME >@ee4e147.ece.ust.hk`

Then, you need to log into the server again by password. And run following codes:

``` shell
chmod 700 .ssh/
chmod 600 .ssh/authorized_keysd
```

Log out the server and you will be all set.  A quick note here is that `chmod` command can help you management the access to folders/documents (you create). The number (i.e. 700/600) is the dummy coding of access. Refer to this [calculator](https://chmod-calculator.com/) for detail. 

## 2. Modules and environment management

### 2.1 Modules

In this server, we use `environment-modules` to manage all pacakages/software installed, and use `Anaconda3` to management the scientific computing environment. 

To load/unload a module that you need, say `matlab`, simply type in command line:

```shell
module load matlab
module unload matlab
```

Then related modules, combined with its environment, will be setup properly. For a complete list of modules and tools in a specific module, please use:

```shell
# Get all module
module avai
# Get details of a module:
module whatis <MODULE NAME>
```

### 2.2 Python environments:

`Python` is the most unstable thing that may cause conflict. A general advice is to run each thing, include different python environments, in separate terminals. It is also to say that only load 1 modules if the is possible. 

Currently, we use a centralize `Anaconda3` to manage all the core things about environment. In other word, you will just use `conda` and some other basic functions. **All your environments will be set on your own directory and separated with others**. Pre-users/Users want to do environment transfer need to start from section a) to c), and new users can directly start from section b).

* a) Archive exsiting environment and remove your anaconda/miniconda completly in ee4e147: Though you may have a python environment, it is recommended to achive that and transfer it to the new system. To do so, 

    * Archive environments: you need to enter your own environment first, say `env_old`. Run `conda env export > <where to save>/env_old.yaml`. This will generate a yaml file, which can be used to transfer your environment.

    * Remove conda completely: Two things need to be done. Firstly, you need to remove the anaconda/miniconda folder in your directory. Secondly, you need to edit you `.bashrc` file and remove the chunk that related to conda (between `>>> conda initialize >>>` and `<<< conda initialize <<<`)

* b) Centralized conda initialization: 
    * To load python in servere, you need to use `module load py3`. Verify that you load the correct python environment by run `which python`. Expected output will be `/usr/local/anaconda3/bin/python`
    * After that, run `conda init zsh` and re-login into the server. Again, verify python environment by run `which python`. Expected output will be `/usr/local/anaconda3/bin/python`. This means that you do not need to load py3 module afterward. If you cannot set environment properly, please contact admin

* c) Environments
    * To enter an environment, please use `conda activate <env>`. To quit that environment, use `conda deactivate`. **NEVER** do any computation without enter into a specific environment. 
    * To recover/copy other environment to your own directory, you need to **create an empty environment** first. Then, you can run `conda env update --name <your new environment name> --f <old environment .yaml file>` to recover the whole conda environment.

## 3. Jupyter Notebook and SoS notebook:

The whole environment `notebook` installed in py3 module. Complete documentation of SoS can be found [here](https://vatlab.github.io/sos-docs/). A demo of that notebook is saved in `/home/Data`. To begin, you need to copy the environment in base to your own directory (just follow steps in 3). **Do not** try to run it in the `Data` directory. When copy the environment, you may see something like pip fail and you can just ignore it. After that, you can copy the demo of that notebook, enter the notebook environment and type `jupyter lab`. Then you can try to run each chunk to see if there is any error. Note that kernels are note that fast on initial running. If you see something wrong on running, just try to restart kernels and notebook first and try to run it again. If some errors persist (mainly will be in matlab), please contact admin.

When using jupyter lab and SoS, you may also want to add an conda environment as a kernel. You can follow [this site](https://stackoverflow.com/questions/53004311/how-to-add-conda-environment-to-jupyter-lab) for install. 



# Appendix

## A.1 Path in Linux:
Path management is the main reason for all setup in the Linux. Consider you are looking for something in a very big pool, it will be very helpful if you someone can give you some direction. The Path in linux is the index to tell the computer where the software is. To see what path you have, type
```shell 
echo $PATH
```
In a **newly opend terminal**. You may see something like `/usr/sbin:/usr/bin:/sbin:/bin`. These are the most important path that store common commands like `ls, cd ...`. The logic of linux is: when you are giving some command. it will start from the first path and search the ideal thing. 

You can do a simple experiment on `python` as follow. Firstly, you need to enter `~/.zshrc` and remove thing betwteen  `>>> conda initialize >>>` and `<<< conda initialize <<<`. After that, re-login. Under this setting, if you type `python`, python 2.7.17 under linux will be open. Then, if you load `py3` module and run `echo $PATH`, you will see two additional path of `anaconda` will be load. In this situation, if you open python again, you will open python 3.9.12 under anaconda. Further, if you activate some environment, you path will be further change (and new pythons, if you specified python version, will be used). You can also try to deactivate environment and unload py3 to see what happened. 

In some case, we may have two packages that share same name or may cause conflict if they are running together. To overcome this and to make the separation of different environment as far as possible, we use `module` to manage all the softwares in this sever. 

## A.2 `~/.bashrc` and `~/.zshrc`

The user interface you see (and changed user interface in section 1.1) is related to `shell`. You can imagine shell as a task (to communicate with sever) and it have  different brunchs (like word and wps, all of them have the task "document processing"). The default shell is called `bash` in Linux, and in section 1.1, we changed that shell to `zsh` for more extentions (like auto suggestion and auto completion) and customizations. This is to say that you need to edit **`~/.zshrc` only** for your future configurations.

The listed two files, `~/.bashrc` and `~/.zshrc` is the two file that control bash shell and zsh shell respectively. They are the two executable that will be run **initially** once you open the shell. That is to say, all the things listed in related `.xxxrc` file will be pre-exsit once you log in. That is to say, if you specify a path in this file, you will not be able to remove it easily (see below). In A.1, we have seen that we can use module to change the path dynamically, so none of them are written in `.xxxrc` file. Upon setup, the only thing in `~/.zshrc` file is the location of the software module.

Utilize this file is very tricky. If you have previous experience of `anaconda`, you may notice that something start and end with `>>> conda initialize >>>` and `<<< conda initialize <<<` is in your `.bashrc` file. It is telling the system to address of python managed by anaconda to be there once you login. 

Further, if you do really want to make some change and let it happend now, you can firstly edit `~/.zshrc` file. After you save it, there will be no changes happened. You need to run `source ~/.zshrc` that tell Linux to stage your change. 