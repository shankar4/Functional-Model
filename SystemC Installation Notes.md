Follow steps here: http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html

The untarred SystemC folder will be in the home directory. Follow the 'install' file. Works fine till the gmake step. There is no gmake on this system. Now, I will follow the steps at the URL above (i.e., sudo make etc). Worked OK. Now, I am switching back to the install step and do a check: sudo make check - This will compile and run the examples in the subdirectory examples. It passed all the 11 tests

Then, back to URL steps: sudo make clean , sudo make -j3, -- done

Next to do: sudo make install in this directory: ~/systemc-2.3.1/objdir
8/10/2018 (continued):
sudo make install

// Tutorials use /usr/local path. I installed in my home directory
// So, had to replce /usr/local with /home/shankar, in a few steps below. 
// I fixed the paths within Eclipse, as given below and the C++ code works.

//Export
export SYSTEMC_HOME=/usr/local/systemc-2.3.1/
sudo gedit /etc/environment 
// and add lines below
SYSTEMC_HOME="/usr/local/systemc-2.3.1/"
export LD_LIBRARY_PATH=/usr/local/systemc-2.3.1/lib-linux64

//gedit accepted these lines, but had some error messages, such as "gedit-encoding not supported
". From forums, it appears that these are harmless. To avoid this problem, use nano or vi, if from command line; else, open gedit from the launcher.
// another possibility is leafpad for command line execution
//sudo apt update
//sudo apt install leafpad
// Another suggestion, helpful for Eclipse.
//sudo apt-get install gksu gedit
//gksu gedit /usr/share/applications/eclipse-oxygen.desktop
//The gksu and gksudo commands allow you to elevate your permissions when running graphical 
//applications. More here: http://www.nongnu.org/gksu/

sudo gedit ~/.bashrc  // the website missed the gedit part in this command
SYSTEMC_HOME="/usr/local/systemc-2.3.1/"
export LD_LIBRARY_PATH=/usr/local/systemc_2.3.1/lib-linux64:$LD_LIBRARY_PATH

//Added these at the end of the file. Same gedit error messages. Could not use the launcher since 
//I could not locate these files!

// Now installing Eclipse
sudo apt-get install eclipse eclipse-cdt g++
//Launch Eclipse through launcher. It must be at the root; but it launches. Put the workspace as
// SystemCSpace
Once Eclipse is open, File->New->Project->c/C++ -> C++. Call it "HelloWorld". Choose  HelloWorld C++ Project and Linux GCC toolchain.
//add paths to systemC folders
Click Project->Properties. Navigate to C/C++ Build -> Settings -> Tool Settings tab.
Under GCC C++ Compiler -> Includes, <click on the add icon on top RHS>> -- 'Add' /usr/local/systemc-2.3.1/include to include paths. 

Add systemc dependent library location in C++ linker settings:
Under C++Linker -> libraries,
add /usr/local/systemc-2.3.1/lib-linux to Library Search Paths. 
// I did not find lib-linux, but found lib-linux64 and sysc under /include. So, I included both paths. 
add systemc and m to libraries

// NOTE: I mistakenly installed systemC in shankar directory. So, paths changed to the following
// Instead of /usr/local/systemc-2.3.1/include, use /home/shankar/systemc-2.3.1/
// Instead of /usr/local/systemc-2.3.1/lib-linux, use /home/shankar/systemc-2.3.1/lib-linux64
// and /home/shankar/systemc-2.3.1/include

Reboot the PC
Open the HelloWorld project, build and Run.
// if it does not run, look at the errors. My paths were wrong (were /usr/local -- had to change to /home/shankar). Based on that, I cleaned, and then built, and then did run successfully. It gave this result: !!!Hello World!!!


Start a new project 'Hello SystemC' (use default hello world project and replace the code there) and include this .cpp code:
 //==========================================================================
// Name : Hello.cpp
// Author :
// Version :
// Copyright : Your copyright notice
// Description : Hello World in C++, Ansi-style
//============================================================================

#include <iostream>
using namespace std;
// All systemc modules should include systemc.h header file
#include "systemc.h"
// Hello_world is module name
SC_MODULE (hello_world) {
SC_CTOR (hello_world) {
// Nothing in constructor
}
void say_hello() {
//Print "Hello World" to the console.
cout << "Hello World.\n";
}
};

// sc_main in top level function like in C++ main
int sc_main(int argc, char* argv[]) {
hello_world hello("HELLO");
// Print the hello world
hello.say_hello();
printf("Hello");
return(0);
}

Apparently in Ubuntu 16.04, Monospace 14 has the problem of underscore disappearance. However, it is needed, as with SC_MODULE. Go to Window -> Preferences. Select General -> Appearance -> Colors and Fonts. To change the font, click 'Edit Defult' button. Change to Ubunto-mono and font size to 12. Also, did this (the first one was good for all, but did this for C++ only, just in case): 
To change just the C/C++ font select, select C/C++/Editor/C/C++ Editor Text Font and click the 'Edit' button. Choose monspace 15 to solve this problem. 

Still errors. So, I am going back to the earlier steps and replaced /usr/local with /home/shankar outside of Eclipse (recall the gedit steps). 

May have to redo as per this site: http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html

sudo mkdir /usr/local/systemc-2.3.1
//configure systemc
./configure-prefix=/usr/local/systemc-2.3.1

Before this, do this:
sudo apt-get upgrade
sudo apt-get install build-essential
sudo apt-get update

I could not find the location of the systemc download. I found it under Files/Recent as /tmp/mozilla_shankar0.
tar -xzvf /tmp/mozilla_shankar0/systemc-2.3.1.tgz
permission denied. I guess that is OK. It is already extracted and avaiable. So, this path of making a /usr/local installation was not continued. 

I have left the installation as a top level directory in /home/shankar. I will just update a few places where I have put /usr/local as below:
launch gedit in launcher and open /etc/environment. Could not find it. So, will invoke thru command line again.

sudo gedit /etc/environment
and modify from /usr/local to /home/shankar:
SYSTEMC_HOME="/home/shankar/systemc-2.3.1/"
export LD_LIBRARY_PATH=/home/shankar/systemc-2.3.1/lib-linux64

sudo gedit ~/.bashrc and modify from /usr/local to /home/shankar:
#added by Ravi Shankar for SystemC installation
SYSTEMC_HOME="/home/shankar/systemc-2.3.1/"
export LD_LIBRARY_PATH=/home/shankar/systemc_2.3.1/lib-linux64:$LD_LIBRARY_PATH

Now, it is time to try Eclipse to see if it works.
It did not. So, I went to this site:https://vinaydvd.wordpress.com/2012/05/30/installing-systemc-in-ubuntu/

Looks like this is the culprit: ”/usr/local/systemc-2.3.1/”

Note the double inverted commas going the same way! I just copied. Not sure how to type them in!
Apparently, they are smart quotes. Need to activate the 'compose' key option. Go to System Settings, Text Entry, and Keyboard Settings. There is a small icon in the left bottom middle that shows the mapping. Check out Keyboard Settings. Default has compose option disabled. As per this blog, https://alvinalexander.com/linux-unix/how-to-smart-quotes-on-ubuntu-keystrokes-macros, map right alt to the compose key. Then, in gedit, do this:
“  -  type [Compose][Shift][,] then "
”  -  type [Compose][Shift][.] then "
‘  -  type [Compose][Shift][,] then '
’  -  type [Compose][Shift][.] then '

same as: 
“  -  type [Compose][<] then "
”  -  type [Compose][>] then "
‘  -  type [Compose][<] then '
’  -  type [Compose][>] then '

Will not try for now, since this is not something I will be doing regularly. If my Eclipse run works, then I won't do this. 

Still this problem:
libsystemc-2.3.1.so: cannot open shared
Solution: (from: https://bbs.archlinux.org/viewtopic.php?id=185248)
create a file with .conf extension under /etc/ld.so.conf.d/ -- the file should contain the path to the directory in which the library is located

I created systemc.conf and added the path: /home/shankar/systemc-2.3.1/lib-linux64. 
Then, run ldconfig as root. So, I did: sudo ldconfig. No error message came. Hopefully, all is well. 

Ready to try Eclipse again.

Success!
Result:
Hello SystemC.
Hello

So, the whole process is working (8/10/18)



---------------------------------------------

What is ldconfig: https://www.lifewire.com/ldconfig-linux-command-4093742


ldconfig creates the necessary links and cache (for use by the run-time linker, ld.so) to the most recent shared libraries found in the directories specified on the command line, in the file /etc/ld.so.conf, and in the trusted directories (/usr/lib and /lib). ldconfig checks the header and file names of the libraries it encounters when determining which versions should have their links updated. ldconfig ignores symbolic links when scanning for libraries.

ldconfig will attempt to deduce the type of ELF libs (ie. libc 5.x or libc 6.x (glibc)) based on what C libraries if any the library was linked against, therefore when making dynamic libraries, it is wise to explicitly link against libc (use -lc). ldconfig is capable of storing multiple ABI types of libraries into a single cache on architectures which allow native running of multiple ABIs, like ia32/ia64/x86_64 or sparc32/sparc64.

Some existing libs do not contain enough information to allow the deduction of their type, therefore the /etc/ld.so.conf file format allows the specification of an expected type. This is only used for those ELF libs which we can not work out. The format is like this "dirname=TYPE", where type can be libc4, libc5 or libc6. (This syntax also works on the command line). Spaces are not allowed. Also see the -p option.

Directory names containing an = are no longer legal unless they also have an expected type specifier.

ldconfig should normally be run by the super-user as it may require write permission on some root owned directories and files. If you use -r option to change the root directory, you don't have to be super-user though as long as you have sufficient right to that directory tree.

#### Continued with RTL and behavioral level SystemC code examples:

1. Copy 'helloSystemC' and give it the name of 'fullAdder.' This should copy the whole set of paths etc.







