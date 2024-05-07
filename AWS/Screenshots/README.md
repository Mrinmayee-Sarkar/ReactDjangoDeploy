# README #


This README document contains the steps to Deploy ReactJS, Django with MYSQL in AWS on Ubuntu 22.4


### Installing Python 3.11 on Ubuntu 22.04 by using the PPA repository###

Step 1: Update system packages
First, update the system packages in the Ubuntu 22.04 terminal by pressing CTRL+ALT+T:

sudo apt update
Step 2: Install Additional dependencies
Install the necessary prerequisites by using the following command:

Step 3: Adding PPA repository
Add the deadsnakes PPA repository to the system next. The simplest method for installing Python 3.11 is as follows:

sudo add-apt-repository ppa:deadsnakes/ppa
Let's continue with installing Python 3.11.

Step 4: Python 3.11 installation
Use this command to install Python 3.11 on Ubuntu 22.04:

sudo apt install python3.11 -y
Step 5: Validate Python Version
python3.11 --version
Output

Python 3.11.4
On our Ubuntu 22.04 system, we have successfully installed Python 3.11.13, as you can see


### Install Django Web Framework on Ubuntu 22.04 ###

If you wish to install Django using the Ubuntu repositories, the process is very straightforward.

First, update your local package index with apt:

sudo apt update
Next, check which version of Python you have installed. 22.04 ships with Python 3.10 by default, which you can verify by typing:

python3 -V
You should see output like this:

Output
Python 3.10.4
Next, install Django:

sudo apt install python3-django
You can test that the installation was successful by typing:

django-admin --version
Output
3.2.12
This means that the software was successfully installed. You may also notice that the Django version is not the latest stable version. To learn more about how to use the software, skip ahead to learn how to create sample project.

Install with pip in a Virtual Environment
The most flexible way to install Django on your system is within a virtual environment. We will show you how to install Django in a virtual environment that we will create with the venv module, part of the standard Python 3 library. This tool allows you to create virtual Python environments and install Python packages without affecting the rest of the system. You can therefore select Python packages on a per-project basis, regardless of conflicts with other projects’ requirements.

Let’s begin by refreshing the local package index:

sudo apt update
Check the version of Python you have installed:

python3 -V
Output
Python 3.10.4
Next, let’s install pip and venv from the Ubuntu repositories:

sudo apt install python3-pip python3-venv
Now, whenever you start a new project, you can create a virtual environment for it. Start by creating and moving into a new project directory:

mkdir ~/newproject
cd ~/newproject
Next, create a virtual environment within the project directory using the python command that’s compatible with your version of Python. We will call our virtual environment my_env, but you should name it something descriptive:

python3 -m venv my_env
This will install standalone versions of Python and pip into an isolated directory structure within your project directory. A directory will be created with the name you select, which will hold the file hierarchy where your packages will be installed.

To install packages into the isolated environment, you must activate it by typing:

source my_env/bin/activate
Your prompt should change to reflect that you are now in your virtual environment. It will look something like (my_env)username@hostname:~/newproject$.

In your new environment, you can use pip to install Django. Regardless of your Python version, pip should just be called pip when you are in your virtual environment. Also note that you do not need to use sudo since you are installing locally:

pip install django
You can verify the installation by typing:

django-admin --version
Output
4.0.4
Note that your version may differ from the version shown here.

To leave your virtual environment, you need to issue the deactivate command from anywhere on the system:

deactivate
Your prompt should revert to the conventional display. When you wish to work on your project again, re-activate your virtual environment by moving back into your project directory and activating:

cd ~/newproject
source my_env/bin/activate



### Install ReactJS on Ubuntu 22.04 ###

Prerequisites
A server with Ubuntu 22.04 as OS
An NVMe VPS with a minimum of 2GB of RAM
User privileges: root or non-root user with sudo privileges
Step 1. Update the System
Before we start with the installation, we need to update the system packages to the latest versions available.

sudo apt-get update -y && sudo apt-get upgrade -y
Step 2. Install NodeJS
NodeJS is an open-source, cross-platform Javascript runtime environment required for the ReactJS application. To install NodeJS execute the following commands:

curl -sL https://deb.nodesource.com/setup_18.x -o nodesource_setup.sh

sudo bash nodesource_setup.sh

sudo apt-get install -y nodejs

After installation, check the installed Node version:

node -v
You should get the following output:

root@host:~# node -v
v18.16.1
Automatically with this installation, the system will install an NPM. NPM is a package manager for Javascript programming. To check the installed NPM version, execute the following command:

npm -v
You should get the following output:

root@host:~# npm -v
9.5.1
To update NPM to the latest version available, execute the following command:

npm install npm@latest -g
Now, the latest NPM version should be:

root@host:~# npm -v
9.7.2
Step 3. Install ReactJS and Create an Application
We need to install the ReactJS package necessary for creating ReactJS projects. To do this, execute the following command:

npm install -g create-react-app
After installation, check the installed version:

create-react-app --version
You should get the following output:

root@host:~# create-react-app --version
5.0.1
To create the ReactJS application, run the following command:

create-react-app rosehosting-project
Once created, you should receive output similar to this:

root@host:~# create-react-app rosehosting-project

Creating a new React app in /root/rosehosting-project.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...
    .
    .
    .
Success! Created rosehosting-project at /root/rosehosting-project
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd rosehosting-project
  npm start

Happy hacking!
