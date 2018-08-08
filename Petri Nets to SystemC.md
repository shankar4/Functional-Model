[O'Hara et al.](http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1002530), (2016) have developed a biologist friendly pathway modeling language (mEPN) that entry level biology professionals can use to visually construct and formalize what they know in a form that can be communicated to their peers. This tool and results will be discussed in a separate folder entitled 'Biological Pathway Models.' Here the emphasis is on their underlying formal modeling approach for dynamic simulations, namely Petri Nets. I discuss here two papers on porting Petri Nets to SystemC.

A [Petri net](https://en.wikipedia.org/wiki/Petri_net) (PN) is a modeling language used to describe concurrent and distributed systems with discrete event dynamics. It is a directed bipartite graph, that uses tokens to represent the activity (or amount) of a given component and a rule-based approach to model the flow of these tokens through a system. PN has two types of vertices: places (represented as circles) and transitions (represented as bars), with a recurrent structure of place-transition-place. Places model conditions, and may contain a discrete number of marks or tokens. A transition can fire based on the local sets of tokens at the places it is connected to and a set of firing rules. Firing consumes the required input tokens and creates tokens in its output places. A firing is atomic (a single non-interruptible step). Unless specified otherwise, a PN executes nondeterministically, i.e., if multiple transitions are enabled at a given time in different parts of the network, they can fire in any order. This also implies that there is no determinstic output, given that the time-sequence of firing is not determinstic. 

Signaling Petri Nets (SPN), that O'Hara et al used in mEPN, was originally developed for network visualization and analysis software BioLayout Express. This software was free in 2016 and has now been replaced with a [commercial product](https://kajeka.com/biolayout-express-upgrade/). It is thus unclear whether mEPN is usable. I will explore that soon. 

However, my goal here was to use mEPN as a frontend tool to capture biologist-centric biological pathway models as a PN structure and port it to SystemC, which is based on C++ and will remain free to use. SystemC also provides a mechanism to port such pathway models (whether modeled with PN or otherwise) to computationally efficient hardware solutions (such as embedded systems and/or dedicated FPGA/IC implementations) for significant speedup and real-time use. 

Rust's papers listed below discuss PN translation to SystemC. 



References cited above:
1. [Rust, et al.](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=1244548): From High-Level Petri Nets to SystemC
2. [Rust and Rettberg](https://link.springer.com/chapter/10.1007/1-4020-8149-9_19): Automatic Synthesis of SystemC Code from Formal Specifications.
