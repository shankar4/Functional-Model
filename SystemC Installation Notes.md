#### Introduction
I follow steps here for SystemC installation on Ubuntu from this 2016 [tutorial](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html), but modified for installation of SystemC-2.3.2 from [here](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.2.zip). Also, The previous author uses Eclipse 3.8, but today (Sept 2018), we have Eclipse 4.8 (Oxygen) which works just fine with Linux/Ubuntu and SystemC 2.3.2. Ignore comments at stackoverflow that may seem to sugest otherwise. 

There are certain things that are done differently when you get to the part on  Eclipse installation. I will use my specific username (shankar) in all paths presented below. Just change it to your username; rest of the paths should remain the same, assuming you follow similar use of the desktop, home, and /usr/local directories. If certain messages, error messages, etc., are not clear, you are welcome to look at the 'Backup-SystemC Installation Notes' folder. It has all the raw outputs. 

#### First Few Steps
In the Terminal (Bash) window: (in Ubuntu 18, right click on empty space in your desktop, scroll down, and choose the terminal window option)
>sudo apt-get upgrade \
.. it recommends: sudo apt autoremove  #run it. Ignore any OS related error messages \
>sudo apt-get install build-essential  \
sudo apt-get update \


#### SystemC 2.3.2. Installation: 

Copy/move the systemc2.3.2.tgz from the download directory on your PC to the home directory. (Extract with a right click on the folder. A new folder with the same name is created in the home directory (in my case, it is /home/shankar).

**Alternative**: You can also use this command from the terminal window. cd to home directory, if not in it. 
>tar -xzvf systemc-2.3.2.tar.gz \

**Continued here**:
>cd systemc-2.3.2 \
sudo mkdir /usr/local/systemc-2.3.2 \
mkdir objdir \
cd objdir \
sudo ../configure –prefix=/usr/local/systemc-2.3.2 \
export CXX=g++ 

>sudo make \
sudo make clean \
sudo make -j3 \
sudo make install \
export SYSTEMC_HOME=/usr/local/systemc-2.3.2/ 

**Smart quotes are essential for the following steps**. Details are found here [here](https://vinaydvd.wordpress.com/2012/05/30/installing-systemc-in-ubuntu/). But you should be able to just copy and paste from here, if you do not wish to understand
how to obtain smart quotes from your keyhboard \

>sudo gedit /etc/environment \
---and add:
SYSTEMC_HOME=”/usr/local/systemc-2.3.2/” \
export LD_LIBRARY_PATH=/usr/local/systemc-2.3.2/lib-linux64 

>sudo gedit ~/.bashrc \
---and add:
SYSTEMC_HOME=”/usr/local/systemc-2.3.2/” \
export LD_LIBRARY_PATH=/usr/local/systemc-2.3.2/lib-linux64:$LD_LIBRARY_PATH













-------------------
This is a copy of the backup notes. NEED TO KEEP WHAT IS RELEVANT
The untarred SystemC folder will be in the home directory. Follow the 'install' file. Works fine till the gmake step. There is no gmake on this system. Now, I will follow the steps at the URL above (i.e., sudo make etc). Worked OK. Now, I am switching back to the install step and do a check: sudo make check - This will compile and run the examples in the subdirectory examples. It passed all the 11 tests

Then, back to URL steps:

    sudo make clean
    sudo make -j3

Next to do: sudo make install in this directory: ~/systemc-2.3.1/objdir 8/10/2018 (continued):

    sudo make install

Tutorials use /usr/local path. I installed in my home directory - redo soon!
So, had to replce /usr/local with /home/shankar, in a few steps below.
I fixed the paths within Eclipse, as given below and the C++ code works.

Export

    export SYSTEMC_HOME=/usr/local/systemc-2.3.1/
    sudo gedit /etc/environment

#and add lines below

    SYSTEMC_HOME="/usr/local/systemc-2.3.1/"
    export LD_LIBRARY_PATH=/usr/local/systemc-2.3.1/lib-linux64

gedit accepted these lines, but had some error messages, such as "gedit-encoding not supported".
From forums, it appears that these are harmless.
To avoid this problem, use nano or vi, if from command line; else, open gedit from the launcher.
another possibility is leafpad for command line execution

    sudo apt update
    sudo apt install leafpad

Another suggestion, helpful for Eclipse.

    sudo apt-get install gksu gedit
    gksu gedit /usr/share/applications/eclipse-oxygen.desktop

The gksu and gksudo commands allow you to elevate your permissions when running graphical
applications. More here: http://www.nongnu.org/gksu/

    sudo gedit ~/.bashrc
    #note: the website missed the gedit part in this command

    SYSTEMC_HOME="/usr/local/systemc-2.3.1/"
    export LD_LIBRARY_PATH=/usr/local/systemc_2.3.1/lib-linux64:$LD_LIBRARY_PATH

Added these at the end of the file. Same gedit error messages. Could not use the launcher
since I could not locate these files!
