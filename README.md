# Functional-Model
Use of SystemC to explore Functional modeling.
After some exploration of HDLs (Hardware Description Languages), I have decided to move on to SystemC, which is free to download and is more rigorous as a language to support concurrent structures at a higher level of abstraction. My goal is to build a distributed model that respects confidentiality and privacy issues, but allows subgroups to share fully de-identified data for higher level analytics. Results would be shared with individual subgroups along with tool updates so they can derive useful information and share with their physician/scientist mentor. This mentor will also have approval from their local human subjects committee for their interactions, data collection, and other processes that involve their subgroup. This may be similar to the way the polling and vote counting is conducted within the USA. I am yet to learn enough details, but from newspaper articles, it appears to  be decentralized enough to require a concerted effort across multiple levels of the hierarchy to compromise the results. A similar approach here would ensure concerns in building a large database of human clinical data that supports all confidentiality and privacy rules and regulations, but goes beyond in anticipating future trends that might compromise the process. By being diligent and alert, and with continuous feedback from the superparticipants (mentors and subgroup patrons) and participants (community members interested in contributing to the overarching goals and also benefiting from the collective advances made). 

Ref for installation of SystemC on Linux with Eclipse is [here](http://euinovation.blogspot.com/2016/02/systemc-development-of-eclipse-on-linux.html).
Update: 8/10/18: I have installed SystemC and Eclipse IDE on Linux. Raw notes ('SystemC Installation Notes') are included [here](https://github.com/shankar4/Functional-Model/blob/master/SystemC%20Installation%20Notes) (will improve later). I have verified that both C++ and SystemC code run successfully (Hello World and Hello SystemC code). The code is also in the SystemC installation notes. 

I am installing [GTKWave Analyzer](http://gtkwave.sourceforge.net/gtkwave.pdf), as suggested in this [paper](http://www.ijcst.com/vol24/2/mitesh.pdf) on RISC implementation using SystemC. 



Ignore the following: Moved from Verilog to SystemC. Kept the info for future ref. 
Miscellaneous notes:
Ref info for Verilog: [ModelSim](https://www.altera.com/products/design-software/model---simulation/modelsim-altera-software.html) simulator will be used. The starter edition is free; it supports mixed HDL simulations (VHDL, Verilog, and System Verilog) and can synthesize to FPGAs. 
