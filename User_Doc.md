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

* `VScode`: will be introduced later
* `MobaXterm`: A windows tool for better server access, also can link GUI between server and you PC (i.e. open matlab in your PC but run code on server)
* `FileZilla`: Specialized in file transfer between server and pc

## 1. Initial setups

### 1.1 Shell configuration

We use `oh-my-zsh` under `zsh` shell for a better experience of command line. Functions like auto suggestion, command auto completion are installed. For your first login, copy following command and run:

```shell
cp /home/Data/.zsh_config/.zshrc $HOME
source $HOME/.zshrc
```
Then you will see the related change. If you do not like the theme preset, you can edit `.zshrc` file under your home directory by changing the `ZSH_THEME` variable. List of avaiable themes are listed [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes). After change that file, please run 
``` shell
source $HOME/.zshrc
```
Again to allow change. Basically this step tell the server to "save" that change permanatly into `.zshrc` file. You may notice that, if you use `ls` command, you actually do not see this file. This is because the `.` tell linux to hide that document. Similar stratiges are used for folders. To see all the things in a certain directory, you can try `ls -a` of `la` in short. If you go into this file, you may notice that several other setups are in it. This file is the file to be executed each time you log in, so the changes in here will be used each time. 




### 1.2 Login without password

Allow logging in without entering password is a very neat solution for every morning. The basic step here include generate a `key` in your own device and then store the key in the server. You can follow the following steps:


* For Window setup

    - To generate the key, you need to use `PowerShell` and run `ssh-keygen -t rsa`. Type `Enter` for all questions. Then, a key will be generated in your PC at `C:\Users\<username>\.ssh\`. Go into that folder, you will see a file called `id_rsa.pub`. Open that text file and copy the whole key. 

    - Then, you need to edit the accesibility of file `id_rsa.pub`. Right click on that file and enter `Properties/属性（R)`. Go into `Security/安全`. You need to delect all other users except yourself,and set the accessof yourself as read and write only.

    - To send the key to the server, log into the server and create necessary files called `authorized_keys`:
    ```shell
    mkdir .ssh && cd .ssh && touch authorized_keys
    ```
    - After create that file, you need to paste the whole key into that file and save the file.

* For Mac setup, open `Terminal`

    - To generate the key, run `ssh-keygen -t rsa`.
    - To send the key to server, run `ssh-copy-id  <YOUR UST USERNAME >@ee4e147.ece.ust.hk`

Then, you need to log into the server again by password. And run following codes:

``` shell
chmod -R 700 .ssh/
sudo chmod 600 .ssh/authorized_keys
```

Log out the server and you will be all set. 

## 2. Modules and environment management

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


## 3. Environment setup:

Python anaconda environment


## 4. VScode integration:

`VScode` have a very nice plugin that can help you interact with server and directly set (nearly) everything in one software. After 





# Appendix

## A. More about Linux:

Linux is  a 