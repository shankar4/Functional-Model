# Functional-Model
Use of SystemC to explore Functional modeling.
After some exploration of HDLs (Hardware Description Languages), I have decided to move on to SystemC, which is free to download and is more rigorous as a language to support concurrent structures at a higher level of abstraction. My goal is to build a distributed model that respects confidentiality and privacy issues, but allows subgroups to share fully de-identified data for higher level analytics. Results would be shared with individual subgroups along with tool updates so they can derive useful information and share with their physician/scientist mentor. This mentor will also have approval from their local human subjects committee for their interactions, data collection, and other processes that involve their subgroup. This may be similar to the way the polling and vote counting is conducted within the USA. I am yet to learn enough details, but from newspaper articles, it appears to  be decentralized enough to require a concerted effort across multiple levels of the hierarchy to compromise the results. A similar approach here would ensure concerns in building a large database of human clinical data that supports all confidentiality and privacy rules and regulations, but goes beyond in anticipating future trends that might compromise the process. By being diligent and alert, and with continuous feedback from the superparticipants (mentors and subgroup patrons) and participants (community members interested in contributing to the overarching goals and also benefiting from the collective advances made). 

Ref for installation of SystemC on Linux with Eclipse is [here](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html).
Update: 8/10/18: I have installed SystemC and Eclipse IDE on Linux. Raw notes ('SystemC Installation Notes') are included [here](https://github.com/shankar4/Functional-Model/blob/master/SystemC%20Installation%20Notes) (will improve later). I have verified that both C++ and SystemC code run successfully (Hello World and Hello SystemC code). The code is also in the SystemC installation notes. 

I am installing [GTKWave Analyzer](http://gtkwave.sourceforge.net/gtkwave.pdf), as suggested in this [paper](http://www.ijcst.com/vol24/2/mitesh.pdf) on RISC implementation using SystemC. Following the steps in the user guide. Download gtkwave from [here](https://sourceforge.net/projects/gtkwave/) - on a Linux system, you should automatically get a Linux download. Extract and put folder in your home directory. Step 1 in the guide:cd to that directory. Do:  ./configure --prefix=/usr. Error message: Could not find tclConfig.sh. I do have a folder tcltk under /usr/lib. How to install the .sh file is given [here](https://www.linuxquestions.org/questions/linux-newbie-8/where-can-i-find-tclconfig-sh-207239/) - look for stas12 comment. I used: apt list tcl to find the version of tcl I have: 8.6.0+9. Then, sudo apt-get install tcl8.6-dev. It was loaded in /usr/lib/tcl8.6. I retried it thus: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6. Now the error msg:  can't find tkConfig.sh. It is a similar procedure: apt list tk -- mine is 8.6. Then sudo apt-get install tk8.6-dev. Now the tkConfig.sh is in /usr/lib/tk8.6. The new command is: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 -- with-tk=/usr/lib/tk8.6. Now the error message is: install gperf from a ftp site  ftp://ftp.gnu.org/pub/gnu/gperf. I downloaded and extracted (I think the extract command was available via right click on the tar folder)- it is in my home directory. 9/9/18: Continuing after Ubuntu upgrade to Version 18. Instructions on install are [here](http://www.linuxfromscratch.org/blfs/view/7.5/general/gperf.html). cd into the gperf directory and use this as per this [link] (http://www.linuxfromscratch.org/lfs/view/stable/chapter06/gperf.html): ./configure --prefix=/usr . Then run make. Then issue make -j1 check - there were no error messages - I suppose that means all checks are OK. Then this: sudo make install. cd out of the directory. Ready to repeat this for gtkwave. cd to that directory and configure thus: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 --with-tk=/usr/lib/tk8.6 - I think no such --with entry is needed for gperf. I tried ./configure --help to see options. there are with options for tcl and tk, not gperf. Understandable, just making sure. new directory of gperf was automatically located (as it is in /usr). Now, the error message: No package 'gtk+-2.0' found. Need to install gtk+-2.0. Information [here](https://askubuntu.com/questions/765526/how-to-install-gtk2-0). Need to do this: sudo apt-get install gtk2.0 and sudo apt-get install build-essential libgtk2.0-dev . Note: Doing the installs with sudo. Message after the second step: libgtk2.0-dev is already the newest version (2.24.32-1ubuntu1). Also another message: The following packages were automatically installed and are no longer required:linux-headers-4.4.0-131 linux-headers-4.4.0-131-generic .  Use 'sudo apt autoremove' to remove them. Removed them. Now, repeat: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 --with-tk=/usr/lib/tk8.6. No erroe messages! So far so good. Now, ready for **make** , then: **sudo make install**.  Everything went through smoothly. No error messages. Now make sure that the bin directory off the install point is in your path. For example, if the install point is/usr/local, ensure that /usr/local/bin is in your path. Here is how to do that: $ echo $PATH . Result: 
/home/shankar/perl5/bin:/home/shankar/src/edirect:/home/shankar/miniconda3/bin:/home/shankar/bin:/home/shankar/.nvm/versions/node/v4.2.6/bin:/home/shankar/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/fis-gtm/V6.0-003_x86_64
I physically naivigated around and found that gtk is under /usr/bin, not /usr/local/bin, as implied above.  It is listed in the above PATH list. So, I am OK. Now, I can see the app icon in the dot martrix ('show application') on the left bottom. Laucn it from there. But, first you need a vcd dump from a HDL simulation. 

------------------------------------------------------------------------------------------------------------
9/7/18: Earlier note -but relevant: **First upgrading to Ubuntu 18/04, 'Bionic Beaver' as it is available**. Some 3rd parthy entries in my source.list are disabled. Re-enable them later with the 'software properties' tool in the package manager. I had it working as of 9/8/18. There were a few surprises along the way, but all is well now. See Ubuntu.md documentation under Functional Genomics [here](https://github.com/shankar4/Functional-Genomics/blob/master/Tools/Ubuntu.md). There was a big surprise. Eclipse stopped working. At this point I had Ubuntu 18, SystemC 2.3.2 and Eclipse 3.8. The error message on 'java.lang.ClassNotFoundException' led me to this stackoverflow [link](https://stackoverflow.com/questions/3412617/java-lang-classnotfoundexception-org-eclipse-core-runtime-adaptor-eclipsestarte). The suggestion provided there on checking on  jar files listed in eclipse\configuration\config.ini did make sense, but had not worked for some. Exploring other related links led me to discussion on inability to support Eclipse 3.8 any further on Ubuntu (as of 2016, not good old days!). I was ready to give up. However, I contacted Accellera, a non-profit organized to support SystemC activities, I posted this in their forum on SystemC language along with a comment: "Apparently Eclipse support for Ubuntu stopped at version 3.8, not the current 4.x. Support may be lacking going forward. Not sure whether it is worth staying with Eclipse." Ameya Vikram Singh responded thus: "You can download the Latest Eclipse package from their website which does work on Ubuntu 18.04.[Eclipse CDT](http://www.eclipse.org/downloads/packages/release/photon/r/eclipse-ide-cc-developers). Download the package most pertinent to your system.(e.g. Ubuntu 64-bit download the Linux 64-Bit package). The Eclipse IDE is very well supported on latest Linux Environments." I downloaded on desktop and extracted with a right click. I went through installation in a bit more involved manner, as given below. Looks like "sudo apt-get install eclipse eclipse-cdt g++" for some reason downloaded only Eclipse 3.8, not the latest 4.8. I wonder whether I made a mistake. Not sure. Either way, I uninstalled Eclipse as installed (the 3.8 version) and started the installation procedure anew as given below (already downloaded and untarred the installation folder): 

First, I read Eclipse Project Release Notes in the Eclipse installation folder (in my case, it was here: file:///home/shankar/eclipse/cpp-photon/eclipse/readme/readme_eclipse.html),  and online link on [IRC FAQ](http://wiki.eclipse.org/IRC_FAQ#I_just_installed_Eclipse_on_Linux.2C_but_it_does_not_start._What_is_the_problem.3F). I found that openJDK (also called GCJ) available, and almost the default in Ubuntu Linux, does not work with Eclipse. I had to find the JVM with JRE or JDK that was not connected with OpenJDK. I found two entries in the same JVM file. One of them was this: /usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java. I updated the eclipse.ini file located here in the Eclipse installation folder extracted earlier ('eclipse-inst-linux64'):  /home/shankar/Desktop/Install Notes/eclipse-inst-linux64/eclipse-installer/eclipse-inst.ini. This required me to add these two lines, above  the -vmargs line  on two separate lines (see below): 
>-vm \
/usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java \
-vmargs \

The new .ini file looked like this:
>-startup \
plugins/org.eclipse.equinox.launcher_1.4.0.v20161219-1356.jar \
--launcher.library \
plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.551.v20171108-1834 \
--launcher.appendVmargs \
--launcher.XXMaxPermSize \
256M \
-name \
Eclipse Installer \
-data \
@noDefault \
--launcher.GTK_version \
2 \
-vm \
/usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java \
-vmargs \
-Xms256M \
-Xmx1024M \
After saving it, I double clicked on the 'eclipse-inst' at the same level as the eclipse.ini file. this automatically installed the ecllpse folder to /usr/shankar/eclipse. The .exe file will be here: /home/shankar/eclipse/cpp-photon/eclipse/eclipse.exe. I double clicked on it and launched Eclipse and it launched just fine. I directed to my workspace at 'SystemCspace' and tried out my 3 examples. I had to update the links to systemC 2.3.2 libraries now installed under /usr/local (see notes elsewhere), rebuild and run. All of them ran fine. 

For eaay accessibility, I right clicked on this .exe file and copy/pasted it to desktop. Unforuntely, it is a generic diamond symbol and it would be nice to associate with the actual eclipse icon. There was a solution for that [here](http://donovanbrown.com/post/Adding-Eclipse-to-Launcher-on-Ubuntu-1604). Here are the steps, as relevant to my system:
>Open a text editor
    Copy and paste the following text into the editor:
    [Desktop Entry]
    Version=1.0
    Name=Eclipse
    Comment=Java IDE
    Type=Application
    Categories=Development;IDE;
    Exec=/home/{username}/Programs/eclipse/eclipse
    Terminal=false
    StartupNotify=true
    Icon=/home/{username}/Programs/eclipse/icon.xpm
    Name[en_US]=Eclipse
    Update any paths if you extracted Eclipse to a different location
    Save the file as eclipse.desktop in /home/{username}/.local/share/applications/
    Reboot your machine
    Search for Eclipse
    Drag and drop the Eclipse icon to the launcher 


------------------------------------------------------------------------------------------------------
*Ignore the following*: Moved from Verilog to SystemC. Kept the info for future ref. 
Miscellaneous notes:
Ref info for Verilog: [ModelSim](https://www.altera.com/products/design-software/model---simulation/modelsim-altera-software.html) simulator will be used. The starter edition is free; it supports mixed HDL simulations (VHDL, Verilog, and System Verilog) and can synthesize to FPGAs. 
