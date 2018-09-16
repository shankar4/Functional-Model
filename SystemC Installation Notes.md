#### Introduction:
I follow steps here for SystemC installation on Ubuntu from this 2016 [tutorial](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html), but modified for installation of SystemC-2.3.2 from [here](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.2.zip). Also, The previous author uses Eclipse 3.8, but today (Sept 2018), we have Eclipse 4.8 (Oxygen) which works just fine with Linux/Ubuntu and SystemC 2.3.2. Ignore comments at stackoverflow that may seem to sugest otherwise. 

There are certain things that are done differently when you get to the part on  Eclipse installation. I will use my specific username (shankar) in all paths presented below. Just change it to your username; rest of the paths should remain the same, assuming you follow similar use of the desktop, home, and /usr/local directories. If certain messages, error messages, etc., are not clear, you are welcome to look at the 'Backup-SystemC Installation Notes' folder. It has all the raw outputs. 

#### First Few Steps:
In the Terminal (Bash) window: (in Ubuntu 18, right click on empty space in your desktop, scroll down, and choose the terminal window option)
>sudo apt-get upgrade \
.. it recommends: sudo apt autoremove  #run it. Ignore any OS related error messages \
>sudo apt-get install build-essential  \
sudo apt-get update \


#### SystemC 2.3.2. Installation: 

Copy/move the systemc2.3.2.tgz from the download directory on your PC to the home directory. (Extract with a right click on the folder. A new extracted folder with the same name is created in the home directory (in my case, it is /home/shankar).

**Alternative**: You can also use this command from the terminal window. cd to home directory, if not in it. 
>tar -xzvf systemc-2.3.2.tar.gz 

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

**Smart quotes are essential for the following steps**. Details are found [here](https://vinaydvd.wordpress.com/2012/05/30/installing-systemc-in-ubuntu/). But you should be able to just copy and paste from here, if you do not wish to understand
how to obtain smart quotes from your keyhboard 

>sudo gedit /etc/environment \
---and add at the end and save:
SYSTEMC_HOME=”/usr/local/systemc-2.3.2/” \
export LD_LIBRARY_PATH=/usr/local/systemc-2.3.2/lib-linux64 \
---ignore any gedit meta error messages

>sudo gedit ~/.bashrc \
---and add at the end and save:
SYSTEMC_HOME=”/usr/local/systemc-2.3.2/” \
export LD_LIBRARY_PATH=/usr/local/systemc-2.3.2/lib-linux64:$LD_LIBRARY_PATH \
------ignore any gedit meta error messages

#### Eclipse Installation: 
Download the Latest Eclipse package from the Eclipse website: [Eclipse CDT](http://www.eclipse.org/downloads/packages/release/photon/r/eclipse-ide-cc-developers). Download the package most pertinent to your system.(for my Ubuntu 64-bit it was the Linux 64-Bit package). The Eclipse IDE is very well supported on latest Linux Environments (Do not believe the stackoverflow comments otherwise). 

Move/copy this file (eclipse-inst-linux64.tar.gz) from the download folder to the desktop (I put mine in a folder there entitled "Installation Notes"). Extract with a right click. An extracted folder with the same name will appear in the same directory. 

There are two good references to help make sure you install correctly. But if you follow my instructions below, you do not need to read through them. More details in my "Backup-SystemC Installation Notes". The first reference is in the installed eclipse installation directory. My reference is here: file:///home/shankar/eclipse/cpp-photon/eclipse/readme/readme_eclipse.html. The other is an online link on [IRC FAQ](http://wiki.eclipse.org/IRC_FAQ#I_just_installed_Eclipse_on_Linux.2C_but_it_does_not_start._What_is_the_problem.3F). 

I found that openJDK (also called GCJ) available, and almost the default in Ubuntu Linux, does not work with Eclipse. I had to find the JVM with JRE or JDK that was not connected with OpenJDK. I found two entries in the same JVM file. One of them was this: /usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java. I updated the eclipse.ini file located here in the Eclipse installation folder extracted earlier ('eclipse-inst-linux64'): /home/shankar/Desktop/Install Notes/eclipse-inst-linux64/eclipse-installer/eclipse-inst.ini. This required me to add these two lines, above the -vmargs line on two separate lines (see below):

    -vm
    /usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java
    -vmargs \

The new .ini file looked like this:

    -startup
    plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar
    --launcher.library
    plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.551.v20171108-1834
    --launcher.appendVmargs
    --launcher.XXMaxPermSize
    256M
    -name
    Eclipse Installer
    -data
    @noDefault
    --launcher.GTK_version
    2
    -vm
    /usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java
    -vmargs
    -Xms256M
    -Xmx1024M
    After saving it, I double clicked on the 'eclipse-inst' at the same level as the eclipse.ini file. this automatically installed the ecllpse folder to /usr/shankar/eclipse. The .exe file will be here: /home/shankar/eclipse/cpp-photon/eclipse/eclipse.exe. I double clicked on it and launched Eclipse and it launched just fine. I directed to my workspace at 'SystemCspace' and tried out my 3 examples. I had to update the links to systemC 2.3.2 libraries now installed under /usr/local (see notes elsewhere), rebuild and run. All of them ran fine.

For eaay accessibility, I right clicked on this .exe file and copy/pasted it to desktop. Unforuntely, it is a generic diamond symbol and it would be nice to associate with the actual eclipse icon. There was a solution for that here. Here are the steps, as relevant to my system:

cd to /home/shankar/.local/share/applications/ and open gedit with filename of eclipse.desktop, and enter (copy and paste with appropriate change for username in place of shankar):

    [Desktop Entry]
    Version=1.0
    Name=Eclipse
    Comment=Java IDE
    Type=Application
    Categories=Development;IDE;
    Exec=/home/shankar/eclipse/cpp-photon/eclipse/eclipse
    Terminal=false
    StartupNotify=true
    icon=/home/shankar/eclipse/cpp-photon/eclipse/icon.xpm
    Name[en_US]=Eclipse \

Save the file. Reboot your machine. I found the Eclpse icon in the dot matrix at left hand side bottom ('Applications'). it launched correctly when clicked on.

So, I am where I was 4 days ago. Need to try out the many SystemC examples that came with the SystemC 2.3.2 folder. Also, examples from Grotker's book. All this is documented here, lest I forget. Soon, i will put together a tutorial style installation document on Systemc 2.3.2 installation on Ubuntu V 18 using Eclipse 4.8 (Oxygen). It uses Java SDK 8.














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
