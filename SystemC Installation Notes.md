Follow steps here: http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html

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
