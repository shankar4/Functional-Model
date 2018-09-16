I am installing [GTKWave Analyzer](http://gtkwave.sourceforge.net/gtkwave.pdf), as suggested in this [paper](http://www.ijcst.com/vol24/2/mitesh.pdf) on RISC implementation using SystemC. 

Following the steps in the user guide. \
Download gtkwave from [here](https://sourceforge.net/projects/gtkwave/) - on a Linux system, you should automatically get a Linux download. Extract and put folder in your home directory. \
#### Step 1 in the guide:
>cd gtkwave-3.3.93 -- cd to the gtkwave installation directory. Do:  \
./configure --prefix=/usr. 
---Error message: Could not find tclConfig.sh. I did have a folder tcltk under /usr/lib, but no .sh file there. \
How to install the .sh file is given [here](https://www.linuxquestions.org/questions/linux-newbie-8/where-can-i-find-tclconfig-sh-207239/) - look for stas12 comment. 

I used: 
>apt list tcl  -- to find the version of tcl I have: 8.6.0+9. Then, \
sudo apt-get install tcl8.6-dev. It was loaded in /usr/lib/tcl8.6. 

I retried it thus: 
>./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 \
---Now the error msg:  can't find tkConfig.sh. It is a similar procedure: 
>apt list tk -- mine is 8.6. Then \
sudo apt-get install tk8.6-dev \
---Now the tkConfig.sh is in /usr/lib/tk8.6. 

The new command is: 
>./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 -- with-tk=/usr/lib/tk8.6 \
--Now the error message is: install gperf from a ftp site  ftp://ftp.gnu.org/pub/gnu/gperf. 

I downloaded and extracted gperf (extract command was available via right click on the tar folder)- it is in my home directory.Continued  after Ubuntu upgrade to Version 18. 

Instructions on install are [here](http://www.linuxfromscratch.org/blfs/view/7.5/general/gperf.html). \
>cd gperf-3.1 -- cd into the gperf directory and use this as per this [link] (http://www.linuxfromscratch.org/lfs/view/stable/chapter06/gperf.html): \
./configure --prefix=/usr -- Then run: \
make \
make -j1 check -- there were no error messages - I suppose that means all checks are OK. Then this: \
sudo make install \ 
cd ~ -- cd out of the gperf directory. 

Ready to repeat this for gtkwave. 
>cd to that directory and configure thus: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 --with-tk=/usr/lib/tk8.6 - I think no such --with entry is needed for gperf. I tried ./configure --help to see options. there are with options for tcl and tk, not gperf. Understandable, just making sure. new directory of gperf was automatically located (as it is in /usr). Now, the error message: No package 'gtk+-2.0' found. Need to install gtk+-2.0. Information [here](https://askubuntu.com/questions/765526/how-to-install-gtk2-0). Need to do this: sudo apt-get install gtk2.0 and sudo apt-get install build-essential libgtk2.0-dev . Note: Doing the installs with sudo. Message after the second step: libgtk2.0-dev is already the newest version (2.24.32-1ubuntu1). Also another message: The following packages were automatically installed and are no longer required:linux-headers-4.4.0-131 linux-headers-4.4.0-131-generic .  Use 'sudo apt autoremove' to remove them. Removed them. Now, repeat: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 --with-tk=/usr/lib/tk8.6. No erroe messages! So far so good. Now, ready for **make** , then: **sudo make install**.  Everything went through smoothly. No error messages. Now make sure that the bin directory off the install point is in your path. For example, if the install point is/usr/local, ensure that /usr/local/bin is in your path. Here is how to do that: $ echo $PATH . Result: 
/home/shankar/perl5/bin:/home/shankar/src/edirect:/home/shankar/miniconda3/bin:/home/shankar/bin:/home/shankar/.nvm/versions/node/v4.2.6/bin:/home/shankar/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/fis-gtm/V6.0-003_x86_64
I physically naivigated around and found that gtk is under /usr/bin, not /usr/local/bin, as implied above.  It is listed in the above PATH list. So, I am OK. Now, I can see the app icon in the dot martrix ('show application') on the left bottom. Laucn it from there. But, first you need a vcd dump from a HDL simulation. 
