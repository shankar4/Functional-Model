#### Introduction:
I follow steps for SystemC installation on Ubuntu from this 2016 [tutorial](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html), but modified for installation of SystemC-2.3.2 from [here](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.2.zip). Also, The tutorial author uses Eclipse 3.8, but today (Sept 2018), we have Eclipse 4.8 (Oxygen) which works just fine with Linux/Ubuntu and SystemC 2.3.2. Ignore comments at stackoverflow that may seem to sugest otherwise. [Accellera](http://forums.accellera.org/) may have more helpful information about SystemC and Eclipse. This tutorial is for Ubuntu V18, SystemC 2.3.2, Eclipse 4.8 (Oxygen), and  JDK8. Note: The SystemC download has installation instructions here (assuming you untarred in your home directory - replace shankar with your username): /usr/shankar/systemc-2.3.2/INSTALL. There are some differences between the tutorial and the INSTALL instructions. Follow one or the other. 

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

In summary, do not use openJDK (or GCJ) for your JVM in the steps below. You will find another JVM, perhaps from IBM or Oracle. Use that. I used this: /usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java. 

Update the eclipse.ini file located in the Eclipse installation folder extracted earlier ('eclipse-inst-linux64'): /home/shankar/Desktop/Install Notes/eclipse-inst-linux64/eclipse-installer/eclipse-inst.ini. 

Open the file in a text editor (gedit is fine) and add these two lines and save, above the -vmargs line on two separate lines:

>-vm \
/usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java \
-vmargs 

The new .ini file looks like this:

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
**-vm \
/usr/lib/jvm/ibm-java80-jre-x86_64/jre/bin/java** \
-vmargs \
-Xms256M \
-Xmx1024M

After saving it, double click on 'eclipse-inst', found at the same level as the eclipse.ini file. This automatically installs the ecllpse folder to /usr/shankar/eclipse. The .exe file will be here: /home/shankar/eclipse/cpp-photon/eclipse/eclipse.exe. Double click on it to launch Eclipse and it should launch just fine. Set up your workspace (Mine is labeled 'SystemCspace'). It is time to enter SystemC code and run programs!
 
You can avoid accessing this deeply embedded .exe file by  adding an Eclipse icon to the desktop:
>cd  /home/shankar/.local/share/applications/ \
gedit eclipse.desktop
--and enter and save (copy and paste with appropriate change for username in place of shankar):

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

Reboot your machine. Eclpse icon would be added to the Applications collection (fouiund in the dot matrix at left hand side bottom. it should launch correctly when clicked on.

#### Running SystemC projects on Eclipse:
Launch Eclipse through the desktop launcher ('Applications' section)
Put the workspace as SystemCSpace
Once Eclipse is open, \

    File->New->Project->c/C++ -> C++.
    Call it "HelloWorld".
    Choose HelloWorld C++ Project and Linux GCC toolchain.

Add paths to systemC folders \

    Click Project->Properties.
    Navigate to C/C++ Build -> Settings -> Tool Settings tab.
    Under GCC C++ Compiler -> Includes, >
    -- 'Add' /usr/local/systemc-2.3.2/include to include paths.

Add systemc dependent library location in C++ linker settings: \

    Under C++Linker -> libraries,
    add /usr/local/systemc-2.3.2/lib-linux64 to Library Search Paths.

    add systemc and m to libraries

Reboot the PC Open the HelloWorld project, build and Run.
if it does not run, look at the errors. 
It should give this result: !!!Hello World!!!

Start a new project 'Hello SystemC'
(use default hello world project and replace the code there) and include this .cpp code:\

//========================================================================== // Name : Hello.cpp // Author : // Version : // Copyright : Your copyright notice // Description : Hello World in C++, Ansi-style //============================================================================

    #include
    using namespace std;

All systemc modules should include systemc.h header file \

    #include "systemc.h"
    //Hello_world is module name
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


**Note**: Apparently in Ubuntu, Monospace 14 has the problem of underscore disappearance. However, it is needed, as with SC_MODULE. Looks like this has been taken care of in the latest releases. Either way, check to make sure it is so. If not, make the change. 

>Go to Window -> Preferences. Select General -> Appearance -> Colors and Fonts. \
To change the font, click 'Edit Defult' button. Change to Ubunto-mono and font size to 12. 

*Note: The following two lines do not make sense. Ignore - taken from a posting; may be wrong. Also should not be needed*:
For C++ only, just in case:
>select C/C++/Editor/C/C++ Editor Text Font and click the 'Edit' button. Choose monspace 12.

I have three projects that are fully functional [here](https://github.com/shankar4/Functional-Model/tree/master/SystemC%20Examples). Download and import into Excel, build and run.

#### Next Step: Installation of the Graphical viewer and updating the adder example for vcd dump
That is documented separately. 

