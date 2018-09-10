# Functional-Model
Use of SystemC to explore Functional modeling.
After some exploration of HDLs (Hardware Description Languages), I have decided to move on to SystemC, which is free to download and is more rigorous as a language to support concurrent structures at a higher level of abstraction. My goal is to build a distributed model that respects confidentiality and privacy issues, but allows subgroups to share fully de-identified data for higher level analytics. Results would be shared with individual subgroups along with tool updates so they can derive useful information and share with their physician/scientist mentor. This mentor will also have approval from their local human subjects committee for their interactions, data collection, and other processes that involve their subgroup. This may be similar to the way the polling and vote counting is conducted within the USA. I am yet to learn enough details, but from newspaper articles, it appears to  be decentralized enough to require a concerted effort across multiple levels of the hierarchy to compromise the results. A similar approach here would ensure concerns in building a large database of human clinical data that supports all confidentiality and privacy rules and regulations, but goes beyond in anticipating future trends that might compromise the process. By being diligent and alert, and with continuous feedback from the superparticipants (mentors and subgroup patrons) and participants (community members interested in contributing to the overarching goals and also benefiting from the collective advances made). 

Ref for installation of SystemC on Linux with Eclipse is [here](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html).
Update: 8/10/18: I have installed SystemC and Eclipse IDE on Linux. Raw notes ('SystemC Installation Notes') are included [here](https://github.com/shankar4/Functional-Model/blob/master/SystemC%20Installation%20Notes) (will improve later). I have verified that both C++ and SystemC code run successfully (Hello World and Hello SystemC code). The code is also in the SystemC installation notes. 

I am installing [GTKWave Analyzer](http://gtkwave.sourceforge.net/gtkwave.pdf), as suggested in this [paper](http://www.ijcst.com/vol24/2/mitesh.pdf) on RISC implementation using SystemC. Following the steps in the user guide. Download gtkwave from [here](https://sourceforge.net/projects/gtkwave/) - on a Linux system, you should automatically get a Linux download. Extract and put folder in your home directory. Step 1 in the guide:cd to that directory. Do:  ./configure --prefix=/usr. Error message: Could not find tclConfig.sh. I do have a folder tcltk under /usr/lib. How to install the .sh file is given [here](https://www.linuxquestions.org/questions/linux-newbie-8/where-can-i-find-tclconfig-sh-207239/) - look for stas12 comment. I used: apt list tcl to find the version of tcl I have: 8.6.0+9. Then, sudo apt-get install tcl8.6-dev. It was loaded in /usr/lib/tcl8.6. I retried it thus: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6. Now the error msg:  can't find tkConfig.sh. It is a similar procedure: apt list tk -- mine is 8.6. Then sudo apt-get install tk8.6-dev. Now the tkConfig.sh is in /usr/lib/tk8.6. The new command is: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 -- with-tk=/usr/lib/tk8.6. Now the error message is: install gperf from a ftp site  ftp://ftp.gnu.org/pub/gnu/gperf. I downloaded and extracted (I think the extract command was available via right click on the tar folder)- it is in my home directory. 9/9/18: Continuing after Ubuntu upgrade to Version 18. Instructions on install are [here](http://www.linuxfromscratch.org/blfs/view/7.5/general/gperf.html). cd into the gperf directory and use this as per this [link] (http://www.linuxfromscratch.org/lfs/view/stable/chapter06/gperf.html): ./configure --prefix=/usr . Then run make. Then issue make -j1 check - there were no error messages - I suppose that means all checks are OK. Then this: sudo make install. cd out of the directory. Ready to repeat this for gtkwave. cd to that directory and configure thus: ./configure --prefix=/usr --with-tcl=/usr/lib/tcl8.6 -- with-tk=/usr/lib/tk8.6

repeat: make , then: sudo make install.  

9/7/18: **First upgrading to Ubuntu 18/04, 'Bionic Beaver' as it is available**. Some 3rd parthy entries in my source.list are disabled. Re-enable them later with the 'software properties' tool in the package manager. I had it working as of 9/8/18. There were a few surprises along the way, but all is well now. See Ubuntu.md documentation under Functional Genomics [here](https://github.com/shankar4/Functional-Genomics/blob/master/Tools/Ubuntu.md).

------------------------------------------------------------------------------------------------------
*Ignore the following*: Moved from Verilog to SystemC. Kept the info for future ref. 
Miscellaneous notes:
Ref info for Verilog: [ModelSim](https://www.altera.com/products/design-software/model---simulation/modelsim-altera-software.html) simulator will be used. The starter edition is free; it supports mixed HDL simulations (VHDL, Verilog, and System Verilog) and can synthesize to FPGAs. 
